---

copyright:
  years: 2024, 2026
lastupdated: "2026-07-01"

keywords: linux, powervs

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent in Linux on {{site.data.keyword.powerSys_notm}}
{: #agent-deploy-linux-powervs}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your Linux hosts on [{{site.data.keyword.powerSysFull}}](/docs/power-iaas?topic=power-iaas-getting-started) to collect events and protect your workloads.
{: shortdesc}

## Adding an agent to a Linux host on {{site.data.keyword.powerSys_notm}}
{: #powervs-linux-add}

Complete the following steps to add an agent to a Linux host on {{site.data.keyword.powerSys_notm}}:

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key).

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion
).

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
   :   The public or private ingestion URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion
). For example, `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`.
   
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

## Updating the agent
{: #powervs-linux-update-agent}

To update the {{site.data.keyword.sysdigsecure_short}} agent, complete the following steps:

1. Clear the yum cache by running the following command:

   ```sh
   sudo yum clean expire-cache
   ```
   {: pre}

2. Update the agent by running the following command:

   ```sh
   sudo yum -y install draios-agent
   ```
   {: pre}

## Removing the agent
{: #powervs-linux-remove-agent}

To remove the {{site.data.keyword.sysdigsecure_short}} agent, run the following command:

```sh
sudo yum erase draios-agent
```
{: pre}


## Checking the agent status
{: #powervs-linux-check-status}

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
{: #powervs-linux-view-logs}

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
