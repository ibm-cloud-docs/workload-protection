---
copyright:
  years: 2024, 2026
lastupdated: "2026-07-01"

keywords:

subcollection: workload-protection
---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent on Windows servers
{: #agent-deploy-windows}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your Windows servers to collect events and protect your workloads.
{: shortdesc}

For examples of threat detection on Windows and troubleshooting detected events, see [Windows Threat Detection with {{site.data.keyword.sysdigsecure_full_notm}}](https://community.ibm.com/community/user/blogs/victor-guerrero/2024/01/11/windows-threat-detection-with-ibm-security-and-com?CommunityKey=dd1ee2bc-c83b-4afb-bd1c-9095ff0c3bc1){: external}.
{: tip}

## Before you begin
{: #agent-deploy-windows-prereqs}

Complete the following steps:

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key) for your {{site.data.keyword.sysdigsecure_short}} instance.

2. Obtain the ingestion URL for your instance. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion).

3. Verify that you have `Administrator` permissions on the Windows server.

## Downloading the agent
{: #agent-deploy-windows-download}

The {{site.data.keyword.sysdigsecure_short}} agent uses Falco to ensure workload security and compliance. The agent has two components: the Connection Manager and the Security Manager, which are both managed by the Agent Installer.

You can install the {{site.data.keyword.sysdigsecure_short}} agent by using either the GUI or the CLI.

[Download the agent](https://download.sysdig.com/stable/msi/x86_64/sysdig-host-shield-latest.msi){: external} in MSI format. If you need to install the agent on a host that runs only in the IBM private network, [download it from IBM Cloud Object Storage](https://s3.direct.us-south.cloud-object-storage.appdomain.cloud/agent-asset-prod-us-south/stable/msi/x86_64/sysdig-host-shield-latest.msi){: external}.

## Installing the agent by using the GUI
{: #agent-deploy-windows-threats-gui}

To install the agent by using the GUI:

1. Run the MSI installer.

2. Accept the EULA.

3. Select **custom** as the region.

4. Complete the following fields:

   Custom Collector
   :   The ingestion URL for the region where your {{site.data.keyword.sysdigsecure_short}} instance is available. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion). For example, `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`.

   Custom Collector port
   :   The collector port. Set to `6443`.

   Custom API URL
   :   The API endpoint URL for the region where your {{site.data.keyword.sysdigsecure_short}} instance is available. For more information, see [API endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_rest_api). For example, `https://private.us-east.security-compliance-secure.cloud.ibm.com`.

   Access Key
   :   The ingestion key for your instance.

5. Complete the installation.

## Installing the agent by using the CLI
{: #agent-deploy-windows-threats-cli}

To install the agent by using the CLI, run the MSI in silent mode from the command line or PowerShell.

Replace `<COLLECTOR_URL>`, `<API_ENDPOINT>`, and `<AGENT_ACCESS_KEY>` with the values from your {{site.data.keyword.sysdigsecure_short}} instance:

```text
msiexec /i sysdig-host-shield-latest.msi REGION=custom ACCESS_KEY=<AGENT_ACCESS_KEY> COLLECTOR_URL=<COLLECTOR_URL> COLLECTOR_PORT=6443 API_URL=<API_ENDPOINT> VM_FEATURE_ENABLED=True POSTURE_FEATURE_ENABLED=True ACCEPT_TERMS_CONDITIONS=True /qn
```
{: pre}

Where:

`AGENT_ACCESS_KEY`
:   The ingestion key for your instance.

`COLLECTOR_URL`
:   The ingestion URL for the region where your {{site.data.keyword.sysdigsecure_short}} instance is available. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion). For example, `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`.

`API_ENDPOINT`
:   The API endpoint URL for the region where your {{site.data.keyword.sysdigsecure_short}} instance is available. For more information, see [API endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_rest_api). For example, `https://private.us-east.security-compliance-secure.cloud.ibm.com/api`.
