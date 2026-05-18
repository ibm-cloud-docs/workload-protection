---

copyright:
  years:  2026
last updated: "2026-05-18"

keywords: PowerVS AIX agent, dragent service, and PowerVS Linux agent

Subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my {{site.data.keyword.powerSys_notm}} agent not reporting data?
{: #ts-agent-powervs}
{: troubleshoot}

After you deploy the {{site.data.keyword.sysdigsecure_short}} agent on a Linux or AIX host on {{site.data.keyword.powerSys_notm}}, the host does not appear in **Integrations** > **Data Sources** > **Sysdig Agents**, or no posture, vulnerability, or threat data is visible.
{: tsSymptoms}

The {{site.data.keyword.powerSys_notm}} agent might not report data for one of the following reasons:
{: tsCauses}

- The access key, collector endpoint, or API endpoint is missing or incorrect in the agent configuration.
- The {{site.data.keyword.powerSys_notm}} host cannot reach the {{site.data.keyword.sysdigsecure_short}} collector endpoint on port 6443. {{site.data.keyword.powerSys_notm}} hosts typically require private endpoints and a {{site.data.keyword.dl_short}} or VPN connection to reach {{site.data.keyword.cloud_notm}} services.
- For Linux hosts, the `dragent` service is not running, or kernel headers are not installed.
- For AIX hosts, the `kspm_analyzer` service was not started correctly, or the `NODE_NAME`, `API_ENDPOINT`, or `ACCESS_KEY` environment variables were not set when starting the service.
- For AIX hosts, the binary was downloaded but execution permissions were not applied.

To resolve this issue, complete the following steps:
{: tsResolve}

## For Linux on {{site.data.keyword.powerSys_notm}}
{: #linux-powervs}

1. Check the agent logs for errors:

   ```sh
   grep -i error /opt/draios/logs/draios.log
   ```
   {: pre}

2. Confirm that the `dragent` service is running:

   ```sh
   systemctl status dragent
   ```
   {: pre}

   3. Verify that `/opt/draios/etc/dragent.yaml` contains the correct `customerid`, `collector`, `sysdig_api_endpoint`, `collector_port: 6443`, and `ssl: true` values. The API endpoint must be specified without the `https://` prefix or `/api` suffix.

   4. Confirm that the PowerVS host can reach the private collector endpoint on port 6443. Use a private endpoint for PowerVS deployments, for example `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`.

   5. If vulnerability scanning or posture data is missing but the agent is connected, confirm that `host_scanner.enabled: true` and `kspm_analyzer.enabled: true` are set in `dragent.yaml`.

## For AIX on {{site.data.keyword.powerSys_notm}}
{: #AIX-powervs}

1. Check the `kspm_analyzer` service logs:

   ```sh
   cat /tmp/kspm-analyzer.log
    ```
   {: pre}

2. Confirm that the binary has execution permissions:

   ```sh
   ls -l /tmp/kspm-analyzer-aix-ppc64
   ```
   {: pre}

   If the execute bit is not set, run:

   ```sh
   chmod +x /tmp/kspm-analyzer-aix-ppc64
   ```
   {: pre}

3. Confirm that the `kspm_analyzer` service is running:

   ```sh
   lssrc -s kspm_analyzer
    ```
   {: pre}

4. If the service is stopped, restart it with the correct environment variables. Replace `<HOSTNAME>`, `<REGION>`, and `<ACCESS_KEY>` with your values:

 ```sh
   startsrc -s kspm_analyzer -e 'NODE_NAME=<HOSTNAME> API_ENDPOINT=<REGION>.security-compliance-secure.cloud.ibm.com ACCESS_KEY=<ACCESS_KEY>'
   ```
   {: pre}

5. Note that the AIX agent supports only posture management (CIS AIX Benchmark). Vulnerability scanning and threat detection are not available for AIX hosts.

For more information, see [Managing the {{site.data.keyword.sysdigsecure_short}} agent in Linux on PowerVS](/docs/workload-protection?topic=workload-protection-agent-deploy-linux-powervs) and [Managing the {{site.data.keyword.sysdigsecure_short}} agent in AIX on PowerVS](/docs/workload-protection?topic=workload-protection-agent-deploy-aix-powervs).
