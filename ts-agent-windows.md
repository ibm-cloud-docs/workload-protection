---

copyright:
  years:  2026
lastupdated: "2026-06-16"

keywords: Windows Server, Windows agent, and collector endpoint

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my Windows agent not reporting data to the dashboard?
{: #ts-agent-windows}
{: troubleshoot}

After you install the {{site.data.keyword.sysdigsecure_short}} agent on a Windows host, the host does not appear in **Integrations** > **Data Sources** > **Sysdig Agents**, or no data appears in the dashboard.
{: tsSymptoms}

The Windows agent might not report data for one of the following reasons:
{: tsCauses}

- The `SysdigHostShield` Windows service did not start after installation.
- The access key or collector endpoint that is entered during installation is incorrect.
- Outbound traffic to the collector endpoint on port 6443 is blocked by Windows Firewall or a network security group.
- The MSI installation completed with errors that were not surfaced during the GUI installation.

To resolve this issue, complete the following steps:
{: tsResolve}

1. Open the Windows Services panel and confirm that the `SysdigHostShield` service is running. If the service is stopped, start it manually.

2. Open a PowerShell window as Administrator and check the service status:

   ```powershell
   Get-Service -Name SysdigHostShield
   ```
   {: pre}

3. Review the Windows Event Viewer for errors related to `SysdigHostShield`.

4. Confirm that the access key and [collector endpoint](/docs/workload-protection?topic=workload-protection-regions#endpoints_ingestion) are correct. You can reinstall the MSI from the command line and pass the correct values:

   ```powershell
   msiexec /i sysdig-host-shield.msi /qn ACCESS_KEY="<ACCESS_KEY>" COLLECTOR_URL="<COLLECTOR_ENDPOINT>" COLLECTOR_PORT="6443"
   ```
   {: pre}

5. Verify that outbound TCP traffic to the collector endpoint on port 6443 is permitted through Windows Firewall and any network security groups attached to the host.

6. After confirming the service is running, wait 2 to 3 minutes, then check **Integrations** > **Data Sources** > **Sysdig Agents** in the {{site.data.keyword.sysdigsecure_short}} UI to verify the agent appears.

For more information, see [Deploying the {{site.data.keyword.sysdigsecure_short}} agent on Windows](/docs/workload-protection?topic=workload-protection-agent-deploy-windows).
