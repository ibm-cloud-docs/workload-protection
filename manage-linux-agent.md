---

copyright:
  years:  2023, 2026
lastupdated: "2026-07-01"

keywords: workload protection, deploy, linux

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# On other Linux hosts
{: #manage-linux-agent}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your Linux hosts to collect events and protect your workloads. You can configure which threats you want to detect in each environment and conduct forensic processes to understand security breaches.
{: shortdesc}

You can protect your hosts running on {{site.data.keyword.cloud_notm}}, other cloud providers such as Amazon Web Services, Azure, Google Cloud Platform, or on-premises by using {{site.data.keyword.sysdigsecure_short}}. Support exists for installing the {{site.data.keyword.sysdigsecure_short}} agent using a package on Debian, Ubuntu, CentOS, RHEL, Fedora, Amazon AMI, and Amazon Linux 2. For information about deploying the agent on Linux hosts running on {{site.data.keyword.powerSysFull}}, see [Managing the {{site.data.keyword.sysdigsecure_short}} agent on Linux on {{site.data.keyword.powerSys_notm}}](/docs/workload-protection?topic=workload-protection-agent-deploy-linux-powervs).
{: tip}

## Adding an agent to a Linux host by using a script
{: #manage-linux-agent-deploy-script}

Complete the following steps to add an agent to a Linux host by using a script:

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key).

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion).

3. Install the kernel headers. When you install a {{site.data.keyword.sysdigsecure_short}} agent, the agent uses kernel header files. Choose a distribution and run the corresponding command.
  
   For Debian and Ubuntu Linux distributions, run the following command:

   ```sh
   apt-get -y install linux-headers-$(uname -r)
   ```
   {: pre}

   For RHEL, CentOS, and Fedora Linux distributions, run the following command:

   ```sh
   yum -y install kernel-devel-$(uname -r)
   ```
   {: pre}
  
4. Deploy the {{site.data.keyword.sysdigsecure_short}} agent by running the following command:

   ```sh
   curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- -a ACCESS_KEY -c COLLECTOR_ENDPOINT --collector_port 6443 --tags TAG_DATA --secure true --additional_conf 'sysdig_api_endpoint: API_ENDPOINT\nhost_scanner:\n  enabled: true\n  scan_on_start: true\nkspm_analyzer:\n  enabled: true'
   ```
   {: pre}
  
   Where:
  
   `ACCESS_KEY`
   :   The ingestion key for the instance.
   
   `COLLECTOR_ENDPOINT`
   :   The public or private ingestion URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion). For example, `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`.
   
   `API_ENDPOINT`
   :   The public or private API endpoint URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [API endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_rest_api). Specify the endpoint without `https://` or `/api`. For example, `private.us-east.security-compliance-secure.cloud.ibm.com`.
   
   `TAG_DATA`
   :   Comma-separated tags that are formatted as `TAG_NAME:TAG_VALUE`. You can associate one or more tags with your {{site.data.keyword.sysdigsecure_short}} agent. For example, `role:serviceX,location:us-south`.
  
   To install cURL, run `yum -q -y install curl` for RHEL, CentOS, and Fedora Linux distributions.
   {: tip}

5. Verify that the {{site.data.keyword.sysdigsecure_short}} agent is running by running the following command:

   ```sh
   ps -ef | grep sysdig
   ```
   {: pre}

6. Check the agent logs. The latest {{site.data.keyword.sysdigsecure_short}} agent logs are located in the `/opt/draios/logs` directory in the `draios.log` file.

   To look for errors, run the following command:

   ```sh
   grep error /opt/draios/logs/draios.log
   ```
   {: pre}

## Adding an agent to a Linux host by using a package
{: #manage-linux-agent-deploy-package}

You can also install the {{site.data.keyword.sysdigsecure_short}} agent manually by installing the package and defining the configuration.

### Adding an agent to Debian or Ubuntu
{: #manage-linux-agent-deploy-package-debian}

Complete the following steps to add an agent to a Debian or Ubuntu Linux host:

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key).

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion).

3. Trust the GPG key, configure the `apt` repository, and update the package list by running the following commands:
  
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

4. Install the kernel headers by running the following command:

   ```sh
   apt-get -y install linux-headers-$(uname -r)
   ```
   {: pre}

5. Install the agent package by running the following command:

   ```sh
   apt-get -y install draios-agent
   ```
   {: pre}

6. Configure the agent by adding the access key and collector endpoint:

   ```sh
   echo customerid: ACCESS_KEY >> /opt/draios/etc/dragent.yaml
   echo tags: [TAGS] >> /opt/draios/etc/dragent.yaml
   echo collector: COLLECTOR_URL >> /opt/draios/etc/dragent.yaml
   echo ssl: true >> /opt/draios/etc/dragent.yaml
   echo secure: true >> /opt/draios/etc/dragent.yaml
   ```
   {: pre}

7. Restart the agent by running the following command:

   ```sh
   service dragent restart
   ```
   {: pre}

### Adding an agent to RHEL, CentOS, or Fedora
{: #manage-linux-agent-deploy-package-rhel}

Complete the following steps to add an agent to a RHEL, CentOS, or Fedora Linux host:

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key).

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion).

3. Trust the GPG key and configure the yum repository by running the following command:

   ```sh
   sudo rpm --import https://download.sysdig.com/DRAIOS-GPG-KEY.public && sudo curl -s -o /etc/yum.repos.d/draios.repo https://download.sysdig.com/stable/rpm/draios.repo
   ```
   {: pre}

4. Install the kernel headers by running the following command:

   ```sh
   yum -y install kernel-devel-$(uname -r)
   ```
   {: pre}

5. Install the agent package by running the following command:

   ```sh
   yum -y install draios-agent
   ```
   {: pre}

6. Configure the agent by adding the access key and collector endpoint:

   ```sh
   echo customerid: ACCESS_KEY >> /opt/draios/etc/dragent.yaml
   echo tags: [TAGS] >> /opt/draios/etc/dragent.yaml
   echo collector: COLLECTOR_URL >> /opt/draios/etc/dragent.yaml
   echo ssl: true >> /opt/draios/etc/dragent.yaml
   echo secure: true >> /opt/draios/etc/dragent.yaml
   echo sysdig_api_endpoint: API_ENDPOINT >> /opt/draios/etc/dragent.yaml
   echo host_scanner: >> /opt/draios/etc/dragent.yaml
   echo "  enabled: true" >> /opt/draios/etc/dragent.yaml
   echo "  scan_on_start: true" >> /opt/draios/etc/dragent.yaml
   echo kspm_analyzer: >> /opt/draios/etc/dragent.yaml
   echo "  enabled: true" >> /opt/draios/etc/dragent.yaml
   ```
   {: pre}

7. Enable and start the agent by running the following commands:

   ```sh
   sudo systemctl enable dragent
   ```
   {: pre}

   ```sh
   sudo systemctl start dragent
   ```
   {: pre}

### Verifying the configuration file
{: #manage-linux-agent-verify-config}

Your configuration file (`/opt/draios/etc/dragent.yaml`) should contain the following settings:

```yaml
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
secure: true
```
{: codeblock}

## Updating the agent
{: #manage-linux-agent-update}

To update the {{site.data.keyword.sysdigsecure_short}} agent, complete the following steps based on your Linux distribution.

For Debian and Ubuntu Linux distributions, run the following commands:

```sh
sudo apt-get update
```
{: pre}

```sh
sudo apt-get -y install draios-agent
```
{: pre}

For RHEL, CentOS, and Fedora Linux distributions, run the following commands:

```sh
sudo yum clean expire-cache
```
{: pre}

```sh
sudo yum -y install draios-agent
```
{: pre}

## Removing the agent
{: #manage-linux-agent-removing}

To remove the {{site.data.keyword.sysdigsecure_short}} agent, complete the following steps based on your Linux distribution.

For Debian and Ubuntu Linux distributions, run the following command:

```sh
sudo apt-get remove draios-agent
```
{: pre}

For RHEL, CentOS, and Fedora Linux distributions, run the following command:

```sh
sudo yum erase draios-agent
```
{: pre}

## Checking the agent status
{: #manage-linux-agent-troubleshooting-status-cli}

To check the status of the agent, run one of the following commands:

```sh
service dragent status
```
{: pre}

```sh
systemctl status dragent
```
{: pre}

## Viewing agent logs
{: #manage-linux-agent-troubleshooting-logs}

The latest {{site.data.keyword.sysdigsecure_short}} agent logs are located in the `/opt/draios/logs` directory in the `draios.log` file.

To view logs for vulnerability scanning, run the following command:

```sh
grep host-scanner /opt/draios/logs/draios.log
```
{: pre}

To view logs for posture management, run the following command:

```sh
grep kspm-analyzer /opt/draios/logs/draios.log
```
{: pre}

To look for errors, run the following command:

```sh
grep -i error /opt/draios/logs/draios.log
```
{: pre}
