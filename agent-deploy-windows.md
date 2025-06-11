---
copyright:
  years: 2024
lastupdated: "2025-06-11"

keywords:

subcollection: workload-protection
---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent on Windows Servers
{: #agent-deploy-windows}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your Windows Servers to collect events and protect your workloads.

{{site.data.keyword.sysdigsecure_short}} provides the following features to protect your Windows servers:

- **Threat detection and response**: identify threats and suspicious activity based on application, network and host activity by processing syscall events and investigate with detailed system captures.
- **Posture management**: scan host configuration files for compliance and benchmarks such as CIS Windows Server Benchmarks.
- **Host scanning**: scan host packages, detect the associated vulnerabilities and identify the resolution priority based on available fixed versions and severity.

{: shortdesc}

## Before you begin
{: #agent-deploy-windows-prereqs}

1. [Obtain the access key](/docs/workload-protection?topic=workload-protection-access_key). It will be used later as `AGENT_ACCESS_KEY`.

2. Obtain the public or private ingestion URL. For more information, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion). It will be used later as `COLLECTOR_URL`.

3. Make sure you have `Administrator` permissions to perform the operations.

## Deploying the agent for threat detection and response
{: #agent-deploy-windows-threats}

The {{site.data.keyword.sysdigsecure_short}} agent uses Falco to ensure workload security and compliance. The agent has two components, the Connection Manager and the Security Manager, which are both managed by the Agent Installer.

Installing the {{site.data.keyword.sysdigsecure_short}} agent using either GUI or CLI operation is possible.

[Download the agent](https://download.sysdig.com/stable/msi/x86_64/sysdig-host-shield-latest.msi) in MSI format to start the installation via GUI or CLI. If you need to install the agent in a host that only runs in the IBM private network you can [download it from here](https://s3.direct.us-south.cloud-object-storage.appdomain.cloud/agent-asset-prod-us-south/stable/msi/x86_64/sysdig-host-shield-latest.msi).

### GUI Installation
{: #agent-deploy-windows-threats-gui}

You can execute the MSI using a GUI and the installation process will prompt you to accept the EULA, select Region as `custom` and complete:
- Custom Collector: is the public or private ingestion URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion). For example, `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`.
- Custom Collector port: set it always to `6443`.
- Custom Api Url: is the public or private API Endpoint URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion). For example `https://private.us-east.security-compliance-secure.cloud.ibm.com`.
- Access Key: is the ingestion key for the instance.

### CLI Installation
{: #agent-deploy-windows-threats-cli}

Run the MSI in silent mode via `CommandLine` or `PowerShell` by running the following command. Remember to replace `<COLLECTOR_URL>`, `<API_ENDPOINT>`, `<AGENT_ACCESS_KEY>` with the values from your {{site.data.keyword.sysdigsecure_short}} instance:

```
> msiexec /i sysdig-host-shield-latest.msi  REGION=custom ACCESS_KEY=<AGENT_ACCESS_KEY> COLLECTOR_URL=<COLLECTOR_URL> COLLECTOR_PORT=6443 API_URL=<API_ENDPOINT> VM_FEATURE_ENABLED=True POSTURE_FEATURE_ENABLED=True ACCEPT_TERMS_CONDITIONS=True  /qn
```
{: pre}

Where:

- AGENT_ACCESS_KEY is the ingestion key for the instance.
- COLLECTOR_URL is the public or private ingestion URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion). For example, `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`.
- API_ENDPOINT is the public or private API Endpoint URL for the region where the {{site.data.keyword.sysdigsecure_short}} instance is available. To get an endpoint, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion). For example `https://private.us-east.security-compliance-secure.cloud.ibm.com`.

## Verifying the installation
{: #agent-deploy-windows-verification}

A few minutes after the installation is completed, make sure that:
- The new service should be running in the host: `SysdigHostShield`.
- You can see your Windows server(s) are list in **Integrations / Data Sources - Sysdig Agents** in your {{site.data.keyword.sysdigsecure_short}} instance.
- Your Windows host appears under **Inventory**. You can filter by the hostname (Resource Name) or type of operating system (Platform).
- You have a vulnerability report for your Windows server under Vulnerabilities / Runtime and search for your host by the hostname or type of system (`asset.type is host`).
- The agent will evaluate Windows configuration files to identify failing controls. Enable your desire policy, such as CIS Benchmarks for Windows, under **Policies / Posture Policies**.
- You enable or customize the Threat Detection policies under **Policies / Runtime Policies** in the `Windows Workload` section.

Check out [Windows Threat Detection with IBM Security and Compliance Center {{site.data.keyword.sysdigsecure_short}}](https://community.ibm.com/community/user/blogs/victor-guerrero/2024/01/11/windows-threat-detection-with-ibm-security-and-com?CommunityKey=dd1ee2bc-c83b-4afb-bd1c-9095ff0c3bc1){: external} to see examples of threat detection on Windows and how to troubleshoot detected events.
