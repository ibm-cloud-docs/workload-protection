---

copyright:
  years:  2025
lastupdated: "2025-01-16"

keywords: linux, powervs, workload protection

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the Workload Protection agent in AIX on PowerVS
{: #agent-deploy-aix-powervs}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your AIX hosts on [{{site.data.keyword.powerSysFull}}](/docs/power-iaas?topic=power-iaas-getting-started) to validate your AIX operating system security.
{: shortdesc}

{{site.data.keyword.sysdigsecure_short}} provides the following features to protect your standalone AIX hosts on {{site.data.keyword.powerSys_notm}}:

- **Posture management**: scan host configuration files for compliance and benchmarks such as CIS AIX Benchmark.

## Deploying the agent by running the binary
{: #agent-deploy-aix-powervs-agent-script}

Complete the following steps to configure a {{site.data.keyword.sysdigsecure_short}} agent on AIX for validating your operating system posture. This agent will forward the security findings to an instance of the {{site.data.keyword.sysdigsecure_short}} service:

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key&interface=ui).

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion).

3. Download the binary:

   ```sh
   curl https://s3.us-east-1.amazonaws.com/download.draios.com/dependencies/kspm-analyzer/1.44.17/kspm-analyzer-aix-ppc64 -o /tmp/kspm-analyzer-aix-ppc64
   ```
   {: pre}
  
   **Note**: This command stores the binary under `/tmp`, you can use your desire directory.

4. Configure the service:

   ```sh
   mkssys -p /tmp/kspm-analyzer-aix-ppc64 -s kspm_analyzer -u 0 -e /tmp/kspm-analyzer.log -i /tmp/kspm-analyzer.log -o /tmp/kspm-analyzer.log
   ```
   {: pre}

   Where:
   * `-p` is the full path of your kspm-analyzer binary you have downloaded in step 3.
   * `-s` is the service name.
   * `-i`, `-o` and `-e` to write logs under `/tmp/kspm-analyzer.logs`. You can use any other file for writing the service logs.

5. Start the service. Make sure to replace `<HOSTNAME>`, `<REGION>` and `<ACCESS KEY>`:

   ```sh
   startsrc -s kspm_analyzer -e 'NODE_NAME=<HOSTNAME> API_ENDPOINT=<REGION>.security-compliance-secure.cloud.ibm.com ACCESS_KEY=<ACCESS KEY>'
   ```
   {: pre}

   Where:
   * `HOSTNAME`: it will be used for showing results and your server in Inventory.
   * `REGION`: depending on the region your have deployed {{site.data.keyword.sysdigsecure_short}}. Check step 2.
   * `ACCESS KEY`: from step 1.


6. Configure the service to run during startup (`inittab`):

   ```sh
   mkitab "fkcmd:2:respawn:startsrc -s kspm_analyzer -e 'NODE_NAME=<HOSTNAME> API_ENDPOINT=<REGION>.security-compliance-secure.cloud.ibm.com ACCESS_KEY=<ACCESSKEY>'"
   ```
   {: pre}

7. Verify the service is running by checking the logs under `/tmp/kspm-analyzer.log`.
