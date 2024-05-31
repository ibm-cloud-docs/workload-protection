---

copyright:
  years:  2023, 2024
lastupdated: "2024-05-31"

keywords: workload protection, deploy, linux

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Protecting Linux hosts
{: manage-linux-agent}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your Linux hosts to collect events and protect your workloads. You can configure which threats you want to detect in each environment and conduct forensic processes to understand security breaches.

{{site.data.keyword.sysdigsecure_short}} provides the following features to protect your standalone Linux hosts:

* **Threat detection**: identify threats and suspicious activity based on application, network and host activity by processing syscall events and investigate with detailed system captures.

* **Posture management**: scan host configuration files for compliance and benchmarks such as CIS Linux Benchmark.

* **Host scanning**: scan host packages, detect the associated vulnerabilities and identify the resolution priority based on available fixed versions and severity.

Protect your hosts running on {{site.data.keyword.cloud_notm}}, other cloud providers such as Amazon Web Services, Azure, Google Cloud Platform, or on-premise by using {{site.data.keyword.sysdigsecure_short}}. Support exists for installing the {{site.data.keyword.sysdigsecure_short}} agent using a package on Debian, Ubuntu, CentOS, RHEL, Fedora, Amazon AMI, and Amazon Linux 2.

## Deploying the Linux agent by using a script
{: manage-linux-agent-deploy-script}

Complete the following steps to configure a {{site.data.keyword.sysdigsecure_short}} agent on Linux to collect and forward metrics to an instance of the {{site.data.keyword.sysdigsecure_short}} service:

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
   curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key ACCESS_KEY --collector COLLECTOR_ENDPOINT --collector_port 6443 --tags TAG_DATA'
   ```
   {: pre}
  
  Where:
  
  * `ACCESS_KEY` is the ingestion key for the instance.
  * `COLLECTOR_ENDPOINT` is the public or private ingestion URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion).
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

## Deploying the Linux agent using a package
{: manage-linux-agent-deploy-package}

1. Obtain the access key.

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion).

3. Trust the Sysdig Monitor GPG key, configure the `apt` repository, and update the package list by running the following commands:
  
   ```sh
   curl -s https://download.sysdig.com/DRAIOS-GPG-KEY.public | apt-key add -
   ```
   {: pre}

   ```sh
   curl -s -o /etc/apt/sources.list.d/draios.list http://download.sysdig.com/stable/deb/draios.list
   ```
   {: pre}

   ```sh
   apt-get update
   ```
   {: pre}  

4. Install the kernel headers. When you install a {{site.data.keyword.sysdigsecure_short}} agent, the agent uses kernel header files. Choose a distribution and run the following command for that distribution.  

  * For Debian and Ubuntu Linux distributions, run the following commands:

    ```sh
    apt-get -y install linux-headers-$(uname -r)
    ```
    {: pre}

  * For RHEL, CentOS, and Fedora Linux distributions, run the following command:

    ```sh
    yum -y install kernel-devel-$(uname -r)
    ```
    {: pre}  

5. Install, configure, and restart the Sysdig agent by running the following commands.  

  * For Debian and Ubuntu Linux distributions, run the following commands:

    ```sh
    apt-get -y install draios-agent
    ```
    {: pre}

    ```sh
    echo customerid: ACCESS_KEY >> /opt/draios/etc/dragent.yaml 
    echo tags: [TAGS] >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```sh
    echo collector: COLLECTOR_URL >> /opt/draios/etc/dragent.yaml 
    echo ssl: true >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```sh
    service dragent restart
    ```
    {: pre}

  * For RHEL, CentOS, and Fedora Linux distributions, run the following commands:

    ```sh
    yum -y install draios-agent
    ```
    {: pre}

    ```sh
    echo customerid: ACCESS_KEY >> /opt/draios/etc/dragent.yaml 
    echo tags: [TAGS] >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```sh
    echo collector: COLLECTOR_URL >> /opt/draios/etc/dragent.yaml 
    echo ssl: true >> /opt/draios/etc/dragent.yaml
    ```
    {: pre}

    ```sh
    echo secure: true >> /opt/draios/etc/dragent.yaml
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

## Updating a Linux agent
{: manage-linux-agent-update}

Complete the following steps to update a {{site.data.keyword.sysdigsecure_short}} agent on Linux.

To update the agent from Debian and Ubuntu Linux distributions, run the following commands as the `sudo` user:

```sh
sudo apt-get update
```
{: pre}

```sh
sudo apt-get -y install draios-agent
```
{: pre}

To update the agent from RHEL, CentOS, and Fedora Linux distributions, run the following commands as the `sudo` user:

```sh
yum clean expire-cache
```
{: pre}

```sh
sudo yum -y install draios-agent
```
{: pre}

## Removing a {{site.data.keyword.sysdigsecure_short}} agent that has been deployed as a service in a Linux system
{: manage-linux-agent-removing}

Complete the following steps to remove a {{site.data.keyword.sysdigsecure_short}} agent on Linux.

To uninstall the agent from Debian and Ubuntu Linux distributions, run the following command as the `sudo` user:

```sh
sudo apt-get remove draios-agent
```
{: pre}

To uninstall the agent from RHEL, CentOS, and Fedora Linux distributions, run the following command as the `sudo` user:

```sh
sudo yum erase draios-agent
```
{: pre}

## Troubleshooting the agent
{: manage-linux-agent-troubleshooting}

### Checking the status of an agent by using the CLI
{: manage-linux-agent-troubleshooting-status-cli}

To check the status of an agent, run the following command: 

```sh
service dragent status
```
{: pre}

```sh
systemctl status dragent
```
{: pre}

### Viewing the logs of an agent
{: manage-linux-agent-troubleshooting-logs}

To see the latest {{site.data.keyword.sysdigsecure_short}} agent logs, go to the directory `/opt/draios/logs` and check the log file `draios.log`.

To look for errors, you can run the following command: 

```sh
grep error /opt/draios/logs/draios.log
```
{: pre}

### Verifying the state of the agent
{: manage-linux-agent-troubleshooting-verify-state}

To check that the {{site.data.keyword.sysdigsecure_short}} agent is running, run the following command: 

```sh
ps -ef | grep sysdig
```
{: pre}

## Identifying vulnerabilities in Linux hosts with Host Analyzer
{: manage-linux-agent-identify-vulnerabilities}

{{site.data.keyword.sysdigsecure_short}} provides host and image scanning in Linux hosts, detecting all installed packages and associated vulnerabilities sorted by severity and prioritizing those with a fix available.

After installing the Host Analyzer, review the detected vulnerabilities in your host accessing **Scanning/Hosts** in the {{site.data.keyword.sysdigsecure_short}}. The first scan starts shortly after installation.

It is possible to run the Host Analyzer by using either Docker or as a package.

### Install using Docker
{: manage-linux-agent-identify-vulnerabilities-docker}

To install the Host Analyzer, issue:

```sh
docker run --detach
-e HOST_FS_MOUNT_PATH=/host
-e SYSDIG_ACCESS_KEY=<ACCESS_KEY>
-e SYSDIG_API_URL=<COLLECTOR_ENDPOINT>
-e SCAN_ON_START=true
-v /:/host:ro --uts=host --net=host
quay.io/sysdig/vuln-host-scanner:$(curl -L -s https://download.sysdig.com/scanning/sysdig-host-scanner/latest_version.txt)
```
{: pre}

Where:

Where:
* **ACCESS_KEY** is the ingestion key for the instance.
* **COLLECTOR_ENDPOINT** is the public or private ingestion URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get the endpoint you need to use, check out [API endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_rest_api).
  - For example, if you have {{site.data.keyword.sysdigsecure_short}} service in EU-GB, the **COLLECTOR_ENDPOINT** would be `https://eu-gb.security-compliance-secure.cloud.ibm.com/internal/scanning/scanning-analysis-collector`.
* **SCAN_ON_START** forces a first scan when the Host Scanner initializes.

### Install as a package
{: manage-linux-agent-identify-vulnerabilities-package}

It is also possible to install the Host Analyzer on non-Kubernetes hosts using packages. 

To do this, follow the instructions in the Sysdig tutorial [Vulnerability Host Scanner](https://docs.sysdig.com/en/docs/installation/sysdig-secure/install-agent-components/hosts/packages/vulnerability-host-scanner/){: external}, following all of the [Installation](https://docs.sysdig.com/en/docs/installation/sysdig-secure/install-agent-components/hosts/packages/vulnerability-host-scanner/#installation) steps for RPM-based operating systems and substituting the [{{site.data.keyword.sysdigsecure_short}} API endpoint](https://cloud.ibm.com/apidocs/workload-protection#endpoint-url) for the`<api-url>` in Step 3.

## Scanning for compliance and benchmarks in Linux hosts with KSPM Analyzer
{: manage-linux-agent-scanning-kpsm}

{{site.data.keyword.sysdigsecure_short}} allows you to evaluate your Linux Hosts against several CIS benchmarks such as CIS Distribution Independent Linux Benchmark and compliance policies.

You need to run the Kubernetes Security Posture Management (KSPM) analyzer as a container. To install the KSPM analyzer in a non-Kubernetes environment, you can use:

```sh
docker run -d \
-v /:/host:ro -v /tmp:/host/tmp --privileged \ 
--network host --pid host --env \
ACCESS_KEY=<Sysdig agent access key> \
--env API_ENDPOINT=<workload_protection_api_endpoint> \ quay.io/sysdig/kspm-analyzer:latest \
```
{: pre}

Where:

* **ACCESS_KEY** is the ingestion key for the instance.
* **API_ENDPOINT** is the public or private API endpoint for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [API endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_rest_api). Notice that you don’t need to include “https”.
  - For example, if you have {{site.data.keyword.sysdigsecure_short}} service in `eu-gb`, the `API_ENDPOINT` would be `eu-gb.security-compliance-secure.cloud.ibm.com`.

As soon as it is running, the KSPM Analyzer will evaluate Linux configuration files to identify failing controls from the enabled Policies. You can see all results in **Posture/Compliance** in the **Entire Infrastructure** zone or define specific zones for your Linux hosts under **Policies/Zones**.