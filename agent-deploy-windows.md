---

copyright:
  years:  2024
lastupdated: "2024-07-11"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent on Windows Servers
{: #agent-deploy-windows}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud_notm}}, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your Windows Servers to collect events and protect your workloads.

{{site.data.keyword.sysdigsecure_short}} provides the following features to protect your Windows servers:

- **Threat detection and response**: identify threats and suspicious activity based on application, network and host activity by processing syscall events and investigate with detailed system captures. 

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

[Download the agent](https://download.sysdig.com/stable/msi/x86_64/agent-windows-1.0.0.msi) in MSI format to start the installation via GUI or CLI.

### GUI Installation
{: #agent-deploy-windows-threats-gui}

You can execute the MSI using a GUI and the installation process will prompt you to accept the EULA and enter the Collector and Access Key details.

### CLI Installation
{: #agent-deploy-windows-threats-cli}

Run the MSI in silent mode via `CommandLine` or `PowerShell` by running the following command. Remember to replace `<COLLECTOR_URL>` and `<AGENT_ACCESS_KEY>` with the values from your {{site.data.keyword.sysdigsecure_short}} instance:

```
> msiexec /i sysdig-agent.msi COLLECTOR_URL=<COLLECTOR_URL> COLLECTOR_PORT=6443 ACCESS_KEY=<AGENT_ACCESS_KEY> ACCEPT_TERMS_CONDITIONS=True /qn
```
{: pre}

## Verifying the installation
{: #agent-deploy-windows-verification}

* After installing the {{site.data.keyword.sysdigsecure_short}} agent, two new services should be running in the host: `Sysdig Connection Manager` and `Sysdig Security Manager`.
* Access to your {{site.data.keyword.sysdigsecure_short}} instance and click on **Integrations / Data Sources - Sysdig Agents**. You should see your Windows server(s) listed there.
* Verify, enable or customize the Threat Detection policies under **Policies / Runtime Policies** in the `Windows Workload` section. 

Check out [Windows Threat Detection with IBM Security and Compliance Center {{site.data.keyword.sysdigsecure_short}}](https://community.ibm.com/community/user/cloud/blogs/victor-guerrero/2024/01/11/windows-threat-detection-with-ibm-security-and-com?CommunityKey=dd1ee2bc-c83b-4afb-bd1c-9095ff0c3bc1) to see examples of threat detection on Windows and how to troubleshoot detected events.