---

copyright:
  years:  2025, 2026
lastupdated: "2026-07-01"

keywords: aix, powervs

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent on AIX on {{site.data.keyword.powerSys_notm}}
{: #agent-deploy-aix-powervs}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your AIX hosts on [{{site.data.keyword.powerSysFull}}](/docs/power-iaas?topic=power-iaas-getting-started) to validate your AIX operating system security.
{: shortdesc}

## Adding an agent to an AIX host on {{site.data.keyword.powerSys_notm}}
{: #powervs-aix-add}

Complete the following steps to add an agent to an AIX host on {{site.data.keyword.powerSys_notm}}:

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key).

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion
).

3. Download the KSPM analyzer binary by running the following command:

   ```sh
   curl https://s3.us-east-1.amazonaws.com/download.draios.com/dependencies/kspm-analyzer/1.44.17/kspm-analyzer-aix-ppc64 -o /tmp/kspm-analyzer-aix-ppc64
   ```
   {: pre}
  
   This command stores the binary in the `/tmp` directory. You can use a different directory if needed.
   {: note}

4. Add execution permissions to the binary by running the following command:

   ```sh
   chmod +x /tmp/kspm-analyzer-aix-ppc64
   ```
   {: pre}

5. Configure the service by running the following command:

   ```sh
   mkssys -p /tmp/kspm-analyzer-aix-ppc64 -s kspm_analyzer -u 0 -e /tmp/kspm-analyzer.log -i /tmp/kspm-analyzer.log -o /tmp/kspm-analyzer.log
   ```
   {: pre}

   Where:

   `-p`
   :   The full path to the KSPM analyzer binary that you downloaded in step 3.

   `-s`
   :   The service name.

   `-i`, `-o`, `-e`
   :   The log file location. This example uses `/tmp/kspm-analyzer.log`. You can specify a different file path for the service logs.

6. Start the service by running the following command:

   ```sh
   startsrc -s kspm_analyzer -e 'NODE_NAME=HOSTNAME API_ENDPOINT=REGION.security-compliance-secure.cloud.ibm.com ACCESS_KEY=ACCESS_KEY'
   ```
   {: pre}

   Where:

   `HOSTNAME`
   :   The hostname that identifies your server in the {{site.data.keyword.sysdigsecure_short}} inventory and results.

   `REGION`
   :   The region where your {{site.data.keyword.sysdigsecure_short}} instance is deployed. For example, `us-east` or `eu-de`. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion
).

   `ACCESS_KEY`
   :   The access key that you obtained in step 1.

   For example:

   ```sh
   startsrc -s kspm_analyzer -e 'NODE_NAME=myhostname API_ENDPOINT=us-east.security-compliance-secure.cloud.ibm.com ACCESS_KEY=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
   ```
   {: pre}

7. Configure the service to start automatically during system startup by running the following command:

   ```sh
   mkitab "fkcmd:2:respawn:startsrc -s kspm_analyzer -e 'NODE_NAME=HOSTNAME API_ENDPOINT=REGION.security-compliance-secure.cloud.ibm.com ACCESS_KEY=ACCESS_KEY'"
   ```
   {: pre}

   Replace `HOSTNAME`, `REGION`, and `ACCESS_KEY` with the same values that you used in step 6.

8. Verify that the service is running by checking the logs:

   ```sh
   tail -f /tmp/kspm-analyzer.log
   ```
   {: pre}


## Checking the agent status
{: #powervs-aix-check-status}

To check the status of the agent, run the following command:

```sh
lssrc -s kspm_analyzer
```
{: pre}

## Stopping the agent
{: #powervs-aix-stop-agent}

To stop the agent, run the following command:

```sh
stopsrc -s kspm_analyzer
```
{: pre}

## Restarting the agent
{: #powervs-aix-restart-agent}

To restart the agent, run the following command:

```sh
stopsrc -s kspm_analyzer && startsrc -s kspm_analyzer -e 'NODE_NAME=HOSTNAME API_ENDPOINT=REGION.security-compliance-secure.cloud.ibm.com ACCESS_KEY=ACCESS_KEY'
```
{: pre}

Replace `HOSTNAME`, `REGION`, and `ACCESS_KEY` with your configuration values.

## Removing the agent
{: #powervs-aix-remove-agent}

To remove the agent from an AIX host on {{site.data.keyword.powerSys_notm}}, complete the following steps:

1. Stop the service:

   ```sh
   stopsrc -s kspm_analyzer
   ```
   {: pre}

2. Remove the service from the system:

   ```sh
   rmssys -s kspm_analyzer
   ```
   {: pre}

3. Remove the service from the startup configuration:

   ```sh
   rmitab fkcmd
   ```
   {: pre}

4. Delete the binary file:

   ```sh
   rm /tmp/kspm-analyzer-aix-ppc64
   ```
   {: pre}

### Viewing agent logs
{: #powervs-aix-view-logs}

The agent logs are located in the `/tmp/kspm-analyzer.log` file by default.

To view the logs in real time, run the following command:

```sh
tail -f /tmp/kspm-analyzer.log
```
{: pre}

To search for errors in the logs, run the following command:

```sh
grep -i error /tmp/kspm-analyzer.log
```
{: pre}
