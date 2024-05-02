---

copyright:
  years:  2024
lastupdated: "2024-04-30"

keywords: linux, powervs, workload protection

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the Workload Protection agent in Linux on PowerVS
{: #agent-deploy-linux-powervs}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your Linux hosts on [{{site.data.keyword.powerSysFull}}](/docs/power-iaas?topic=power-iaas-getting-started) to collect events and protect your workloads.
{: shortdesc}

{{site.data.keyword.sysdigsecure_short}} provides the following features to protect your standalone Linux hosts on {{site.data.keyword.powerSys_notm}}:

- **Threat detection and response**: identify threats and suspicious activity based on application, network, and host activity by processing syscall events and investigate with detailed system captures.
- **Posture management**: scan host configuration files for compliance and benchmarks such as CIS Linux Benchmark.
- **Host scanning**: scan host packages, detect the associated vulnerabilities and identify the resolution priority based on available fixed versions and severity.

## Deploying the agent for threat detection and response 
{: #agent-deploy-linux-powervs-agent}

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key).

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion).

3. Make sure `dkms` is installed:

    - For RHEL or CentOS, run the following command:

    ```sh
    sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
    sudo yum install dkms
    ```
    {: pre}

4. Install the kernel headers. When you install a {{site.data.keyword.sysdigsecure_short}} agent, the agent uses kernel header files.
    
    - For RHEL or CentOS, run the following command:

    ```sh
    sudo yum -y install kernel-devel-$(uname -r)
    ```
    {: pre}

5. Trust the GPG key and configure the yum repository:
    
    - For RHEL or CentOS, run the following command:

    ```sh
    sudo rpm --import https://download.sysdig.com/DRAIOS-GPG-KEY.public && sudo curl -s -o /etc/yum.repos.d/draios.repo https://download.sysdig.com/stable/rpm/draios.repo
    ```
    {: pre}

6. Install, configure, and restart the {{site.data.keyword.sysdigsecure_short}} agent by running the following commands:
    
    - For RHEL or CentOS, run the following command:
    
    Install the agent package:

    ```sh
    sudo yum -y install draios-agent
    ```
    {: pre}

    Add the Collector endpoint and the Access Key:
  
    ```sh
    echo customerid: ACCESS_KEY >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```sh
    echo collector: COLLECTOR_URL >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```sh
    sudo systemctl enable dragent
    ```
    {: pre}

    ```sh
    sudo systemctl start dragent
    ```
    {: pre}

Wait a few seconds to make sure the agent is started and access to {{site.data.keyword.sysdigsecure_short}} Data Sources (Integrations > Data Sources | Sysdig Agents) to verify the agent is correctly conencted. 

### Updating the agent
{: #agent-deploy-linux-powervs-update-agent}

Complete the following steps to update a {{site.data.keyword.sysdigsecure_short}} agent on Linux on {{site.data.keyword.powerSys_notm}}.

```sh
sudo yum clean expire-cache
```
{: pre}

```sh
sudo yum -y install draios-agent
```
{: pre}

### Troubleshooting the agent
To see the latest {{site.data.keyword.sysdigsecure_short}} agent logs, go to the directory `/opt/draios/logs` and check the log file `draios.log`.

To look for errors, you can run the following command:

```sh
grep -i error /opt/draios/logs/draios.log
```
{: pre}

## Scanning vulnerabilities in Linux hosts on PowerVS
{: #agent-deploy-linux-powervs-scanning}

{{site.data.keyword.sysdigsecure_short}} provides a scanning component to identify vulnerabilities in your Linux hosts on {{site.data.keyword.powerSys_notm}}. It detects all installed packages and associated vulnerabilities sorted by severity and prioritizing those with a fix available.

After installing the Host Scanner, review the detected vulnerabilities in your host accessing Vulnerabilities / Runtime and filter by `asset.type = host` in {{site.data.keyword.sysdigsecure_short}}. The first scan starts shortly after installation.

You will install the Host Scanner from the binary.

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key).

2. Obtain the public or private API Endpoint. For more information, see [REST API endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_rest_api). **Note**: you need to remove `/api` when configuring step 5, example: `https://us-east.security-compliance-secure.cloud.ibm.com` 

3. Download the binary:

    ```sh
    curl -LO https://download.sysdig.com/scanning/bin/sysdig-host-scanner/$(curl -L -s https://download.sysdig.com/scanning/sysdig-host-scanner/latest_version.txt)/linux/ppc64le/sysdig-host-scanner
    ```
    {: pre}

4. Set the executable flag on the file:

    ```sh
    chmod +x ./sysdig-host-scanner
    ```
    {: pre}

5. You can run once the Host Scanner by running the `sysdig-host-scanner` command:

    ```sh
    SYSDIG_ACCESS_KEY=<access-key> SYSDIG_API_URL=<api-url> SCAN_ON_START=true ./sysdig-host-scanner
    ```
    {: pre}

6. Create an environment file to store the configuration and a systemd unit file to run the binary as a service. Make sure to replace `<access key>` and `<api-url>`:

    ```sh
    sudo mv ./sysdig-host-scanner /usr/local/bin/vuln-host-scanner
    sudo restorecon -Rv /usr/local/bin/vuln-host-scanner
    sudo mkdir -p /opt/draios/etc/vuln-host-scanner/

    cat << EOF | sudo tee /opt/draios/etc/vuln-host-scanner/env
    SYSDIG_ACCESS_KEY=<access-key>
    SYSDIG_API_URL=<api-url>
    SCAN_ON_START=true
    EOF

    cat << EOF | sudo tee /etc/systemd/system/vuln-host-scanner.service
    [Unit]
    Description=Sysdig Vuln Host Scanner component

    [Service]
    EnvironmentFile=/opt/draios/etc/vuln-host-scanner/env
    ExecStart=/usr/local/bin/vuln-host-scanner

    [Install]
    WantedBy=multi-user.target
    EOF

    sudo systemctl daemon-reload
    sudo systemctl enable --now vuln-host-scanner.service
    ```
    {: pre}

7. Now, you can control the Host Scanner via the service `vuln-host-scanner`:
  
    ```sh
    systemctl status vuln-host-scanner
    ```
    {: pre}

After a few minutes, access to {{site.data.keyword.sysdigsecure_short}} Vulnerabilities / Runtime and filter by `asset.type = host` to review the vulnerabilities associated to your host.

## Running posture validation in Linux hosts on PowerVS
{: #agent-deploy-linux-powervs-posture-validation}

{{site.data.keyword.sysdigsecure_short}} allows you to evaluate your Linux hosts on {{site.data.keyword.powerSys_notm}} against several CIS benchmarks such as CIS Distribution Independent Linux Benchmark and compliance policies.

You must run the Kubernetes Security Posture Management (KSPM) analyzer as a container. Podman is an option.

To install the KSPM analyzer in a non-Kubernetes environment:

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key).

2. Obtain the public or private API Endpoint. For more information, see [REST API endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_rest_api). **Note**: you need to remove `/api` and without the protocol when configuring step 3, example: `us-east.security-compliance-secure.cloud.ibm.com` 

3. Run the KSPM analyzer:

    ```sh
    podman run -d -v /:/host:ro -v /tmp:/host/tmp --privileged \
    --network host --pid host --env ACCESS_KEY=<Sysdig agent access key> \
    --env API_ENDPOINT=<workload_protection_api_endpoint> \
    quay.io/sysdig/kspm-analyzer:latest
    ```
    {: pre}

As soon as it is running, the KSPM Analyzer will evaluate Linux configuration files to identify failing controls from the enabled policies. You can see all results in **Posture/Compliance** in the **Entire Infrastructure** zone or define specific zones for your Linux hosts on {{site.data.keyword.powerSys_notm}} under **Policies/Zones**.