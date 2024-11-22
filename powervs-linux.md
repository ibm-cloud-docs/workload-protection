---

copyright:
  years:  2024
lastupdated: "2024-05-03"

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

## Deploying the agent by using a script
{: #agent-deploy-linux-powervs-agent-script}

Complete the following steps to configure a {{site.data.keyword.sysdigsecure_short}} agent on Linux for detecting threats, validating your operating system posture and scanning your server to identify vulnerabilities. This agent will forward all security findings to an instance of the {{site.data.keyword.sysdigsecure_short}} service:

1. Obtain the access key.

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion).

3. Install the kernel headers. When you install a {{site.data.keyword.sysdigsecure_short}} agent, the agent uses kernel header files. Choose a distribution and run the following command for that distribution.
  
   * For Debian and Ubuntu Linux distributions, run the following command:

     ```sh
     apt-get -y install linux-headers-$(uname -r)
     ```
     {: pre}

   * For RHEL, CentOS, and Fedora Linux distributions, run the following command:

     ```sh
     yum -y install kernel-devel-$(uname -r)
     ```
     {: pre}  
  
4. Deploy the {{site.data.keyword.sysdigsecure_short}} agent. Run the following command:

   ```sh
   curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- -a ACCESS_KEY -c COLLECTOR_ENDPOINT --collector_port 6443 --tags TAG_DATA --secure true --additional_conf 'sysdig_api_endpoint: API_ENDPOINT\nhost_scanner:\n  enabled: true\n  scan_on_start: true\nkspm_analyzer:\n  enabled: true'
   ```
   {: pre}
  
  Where:
  
  * `ACCESS_KEY` is the ingestion key for the instance.
  * `COLLECTOR_ENDPOINT` is the public or private ingestion URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion). For example, `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`.
  * `API_ENDPOINT` is the public or private API Endpoint URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_rest_api). Make sure to add it without `https` or `/api`, for example `private.us-east.security-compliance-secure.cloud.ibm.com`.
  * `TAG_DATA` are comma-separated tags that are formatted as `TAG_NAME:TAG_VALUE`. You can associate one or more tags to your {{site.data.keyword.sysdigsecure_short}} agent. For example, `role:serviceX,location:us-south`.
  
  To install cURL, run `yum -q -y` install curl for RHEL, CentOS, and Fedora Linux distributions.  
5. Check that the {{site.data.keyword.sysdigsecure_short}} agent is running. Run the following command:

   ```sh
   ps -ef | grep sysdig
   ```
   {: pre}

To see the latest {{site.data.keyword.sysdigsecure_short}} agent logs, go to the directory `/opt/draios/logs` and check the log file `draios.log`.

To look for errors, issue:

   ```sh
   grep error /opt/draios/logs/draios.log
   ```
   {: pre}  

## Deploying the agent using a package
{: #agent-deploy-linux-powervs-agent-package}

You can also install the {{site.data.keyword.sysdigsecure_short}} agent manually by installing the package and defining all the configuration.

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
    echo sysdig_api_endpoint: API_ENDPOINT >> /opt/draios/etc/dragent.yaml
    echo host_scanner: >> /opt/draios/etc/dragent.yaml
    echo "  enabled: true" >> /opt/draios/etc/dragent.yaml
    echo "  scan_on_start: true" >> /opt/draios/etc/dragent.yaml
    echo kspm_analyzer: >> /opt/draios/etc/dragent.yaml
    echo "  enabled: true" >> /opt/draios/etc/dragent.yaml
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

Your configuration file (`/opt/draios/etc/dragent.yaml`) needs to look like:
```
customerid: ACCESS_KEY
tags: [TAGS]
collector: COLLECTOR_URL
sysdig_api_endpoint: API_ENDPOINT
host_scanner:
  enabled: true
  scan_on_start: true
kspm_analyzer:
  enabled: true
collector_port: 6443
ssl: true
```

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

If you want to see logs for the vulnerability scanning, grep by `host-scanner`. To look for Posture information, grep by `kspm-analyzer`.

To look for errors, you can run the following command:

```sh
grep -i error /opt/draios/logs/draios.log
```
{: pre}

## Verifying results in the UI
{: manage-linux-agent-verify}

After a few minutes, you can check the results in the UI for your Vulnerabilities, the Posture validation and, if any, Threats detected in your host.

Access to your {{site.data.keyword.sysdigsecure_short}} instance:
- Verify your agent is connected correctly under **Integrations / Data Sources / Sysdig Agents**.
- Review your host appears under **Inventory**. You can filter by the hostname (`Resource Name`) or type of operating system (`Platform`)
- The {{site.data.keyword.sysdigsecure_short}} agent will evaluate Linux configuration files to identify failing controls from the enabled Policies. You can see all results in **Posture/Compliance** in the **Entire Infrastructure** zone or define specific zones for your Linux hosts under **Policies/Zones**.
- The {{site.data.keyword.sysdigsecure_short}} agent provides host and image scanning in Linux hosts, detecting all installed packages and associated vulnerabilities sorted by severity and prioritizing those with a fix available. Access to **Vulnerabilities / Runtime** and search for your host by the hostname or type of system (`asset.type is host`).
- As soon as the {{site.data.keyword.sysdigsecure_short}} will start detecting threats based on the Runtime Policies that are configured. Access to **Threats** to see if any event was detected. In this [document](/docs/workload-protection?topic=workload-protection-threat_detection), you can find how to manage the threat detection policies and rules.
