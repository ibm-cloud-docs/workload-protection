---

copyright:
  years: 2026
lastupdated: "2026-06-16"

keywords: cspm, compliance, agents, zones, policies, enterprise accounts

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Best practices for {{site.data.keyword.sysdigsecure_short}}
{: #bp}

Review these best practices to help you get the most out of {{site.data.keyword.sysdigsecure_full}}.
{: shortdesc}

## Cloud security posture management (CSPM)
{: #bp-cspm}

Cloud security posture management (CSPM) helps you continuously assess and improve your cloud security posture by identifying compliance violations across your {{site.data.keyword.cloud_notm}} account and resources. For more information, go to [Managing compliance with CSPM](/docs/workload-protection?topic=workload-protection-cspm-compliance).

### Enable CSPM
{: #bp-cspm-enable}

Enable CSPM to gain visibility into your cloud security posture across all your {{site.data.keyword.cloud_notm}} resources. CSPM automatically discovers and evaluates your cloud resources against security best practices and compliance frameworks.

By default, CSPM is enabled when you create a new {{site.data.keyword.sysdigsecure_short}} instance. Keep CSPM enabled to automatically scan your {{site.data.keyword.cloud_notm}} account and resources for compliance. If you disable CSPM before creating the instance, [you can set up the connection manually later](/docs/workload-protection?topic=workload-protection-cspm-tutorial-enterprise#connect-appconfig). 

### Use built-in compliance frameworks
{: #bp-cspm-frameworks}

{{site.data.keyword.sysdigsecure_short}} provides built-in compliance frameworks such as {{site.data.keyword.framework-fs_full}}, DORA, CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark, and PCI standards. Use these frameworks to assess your compliance posture against industry standards, identify gaps in your security controls, generate compliance reports for audits, and track remediation progress over time.

Start with [predefined policies](/docs/workload-protection?topic=workload-protection-posture-policies-services#predefined-policies) and apply them to appropriate zones. These policies are regularly updated with new parameters and checks. If predefined policies do not meet your requirements, [create custom policies](https://docs.sysdig.com/en/sysdig-secure/manage_posture_policies/#create-a-custom-policy){: external} based on existing or customized controls. Keep policies in draft state while designing and configuring them to avoid affecting running compliance scans. Policies are not run in your environment until they are published.

### Review and prioritize remediation
{: #bp-cspm-remediation}

After the first completed scan, review posture results from **Attack Surface > Compliance Findings**. Not all compliance violations carry the same risk. Focus your remediation efforts by severity, so critical and high-severity findings are addressed first. For more information, see [Findings](https://docs.sysdig.com/en/sysdig-secure/compliance-findings/){: external}. 

Use the [**Inventory**](https://docs.sysdig.com/en/docs/sysdig-secure/inventory/){: external} to review all connected {{site.data.keyword.cloud_notm}} resources and use feature filters to narrow down to your most prevalent and at-risk resources.
{: tip}

## View and schedule reports
{: #bp-cspm-reports}

Built in with {{site.data.keyword.sysdigsecure_short}} is a highly scalable and powerful reporting platform. With it, you can create and schedule reports with large amounts of data for audit purposes. For more information, go to [Reporting](https://docs.sysdig.com/en/docs/sysdig-secure/reporting/){: external}.

## Working with agents
{: #bp-agents}

Agents collect security and compliance data from your workloads. Follow these best practices to ensure optimal agent deployment and management.

### Add agents strategically
{: #bp-agents-deploy}

Deploy agents to all environments where you need security visibility and compliance monitoring:

Kubernetes and OpenShift clusters
:   Deploy agents using Helm charts for easier management and updates. Helm 3.6 or later is required. Create a dedicated namespace (for example, `ibm-observe`) to isolate agents from application workloads.

Virtual servers
:   Install agents on Linux and Windows virtual servers to monitor host-level security.

{{site.data.keyword.satellitelong_notm}} locations
:   Deploy agents to {{site.data.keyword.satelliteshort}}-managed infrastructure for consistent security across hybrid environments.

Power Systems
:   Install agents on AIX and Linux on Power to extend security monitoring to these platforms.

You can use the console to connect an existing {{site.data.keyword.redhat_openshift_notm}} or Kubernetes cluster to your instance of {{site.data.keyword.sysdigsecure_short}}. In the {{site.data.keyword.cloud_notm}} console, go to **Containers > Clusters** to access the existing cluster. Then, click **Connect** in the {{site.data.keyword.sysdigsecure_short}} widget to connect your cluster to {{site.data.keyword.sysdigsecure_short}}.
{: fast-path}

Choose from the following options to add an agent programmatically:
- [Deploying an agent on a Kubernetes cluster](/docs/workload-protection?topic=workload-protection-agent-deploy-kube-helm)
- [Deploying an agent on an OpenShift cluster](/docs/workload-protection?topic=workload-protection-agent-deploy-openshift-helm)
- [Deploying an agent on {{site.data.keyword.satelliteshort}}](/docs/workload-protection?topic=workload-protection-agent-deploy-satellite)
- [Deploying an agent on Linux hosts on Power Virtual Server](/docs/workload-protection?topic=workload-protection-agent-deploy-linux-powervs)
- [Deploying an agent on AIX hosts on Power Virtual Server](/docs/workload-protection?topic=workload-protection-agent-deploy-aix-powervs)
- [Deploying an agent on an outside Kubernetes or Red Hat OpenShift cluster](/docs/workload-protection?topic=workload-protection-deploy-wp-outside-cloud)
- [Deploying an agent on Windows](/docs/workload-protection?topic=workload-protection-agent-deploy-windows)
- [Deploying an agent on a Linux host](/docs/workload-protection?topic=workload-protection-manage-linux-agent)

### Configure agents appropriately
{: #bp-agents-configure}

Customize agent configuration based on your environment and requirements:

eBPF driver
:   Configure the universal eBPF driver when supported. The universal eBPF driver requires kernel version 5.8 or newer. If you have an older version, you need BPF ring buffer support and a kernel that exposes BTF (BPF Type Format). If you encounter problems during agent installation, try removing the eBPF configuration or contact support.

Private endpoints
:   If your security requirements mandate that data does not traverse the public internet, configure agents to use private endpoints. Ensure that virtual routing and forwarding (VRF) is enabled for your account.

Resource allocation
:   Set appropriate CPU and memory limits for agents to prevent resource contention with application workloads. Monitor CPU and memory usage of agents to ensure they do not impact application performance.

Access keys
:   Protect access keys used by agents. Rotate keys periodically and disable unused keys immediately to prevent unauthorized access.

### Keep agents updated
{: #bp-agents-maintain}

Regularly update agents to the latest version to benefit from new features, bug fixes, and security patches. Monitor the [Agent release notes](https://docs.sysdig.com/en/sysdig-agent-release-notes.html){: external} for updates.

### Share an agent with {{site.data.keyword.mon_short}}
{: #bp-agents-sharing}

If you use both {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.mon_full_notm}}, deploy a single agent that works for both products. You can connect them when you create an instance of either service to avoid deploying duplicate agents and optimize costs.

## Zones and policies
{: #bp-zones-policies}

Zones and policies are fundamental to organizing your compliance monitoring and applying the right security controls to your resources.

### Organize resources with zones
{: #bp-zones-organize}

By default, {{site.data.keyword.sysdigsecure_short}} creates a zone called **Entire Infrastructure** for all connected resources. [Create custom zones](https://docs.sysdig.com/en/sysdig-secure/zones/#create-and-configure-a-zone){: external} to organize resources logically for compliance assessments based on business unit, geographic location, compliance requirements, and more.

### Handle context-based restrictions
{: #bp-zones-cbr}

When context-based restrictions are enabled for resources, configuration data cannot be collected unless access is provided. Create appropriate network zones and reference {{site.data.keyword.appconfig_short}} as the reference service to ensure {{site.data.keyword.sysdigsecure_short}} can scan your resources. For more information, see [Creating context-based restrictions](/docs/account?topic=account-context-restrictions-create&interface=ui).

## Enterprise accounts
{: #bp-enterprise}

If you have an {{site.data.keyword.cloud_notm}} enterprise account, follow these best practices to enable comprehensive posture management across all child accounts in your organization.

### Set up trusted profile templates
{: #bp-enterprise-trusted-profiles}

Enterprise accounts must set up a trusted profile template to allow {{site.data.keyword.sysdigsecure_short}} to scan child accounts for compliance. This is a critical requirement for enterprise-wide compliance management with CSPM. For more information, see [Set up App Configuration to collect configuration data from all child accounts](/docs/workload-protection?topic=workload-protection-cspm-tutorial-enterprise#setup-appconfig).

Create zones based on child account IDs to organize and manage compliance reporting for different parts of your enterprise. 
{: tip}

### Enable IAM for enterprise accounts
{: #bp-enterprise-iam}

Enterprise accounts must be IAM-enabled to support trusted profile templates and cross-account scanning. Verify that your enterprise account has IAM enabled before attempting to set up CSPM for child accounts.

### Manage access across the enterprise
{: #bp-enterprise-access}

Implement the principle of least privilege across your enterprise:

- Use [IAM access groups](/docs/enterprise-management?topic=enterprise-management-rgs&interface=ui) to organize users with similar access needs.
- Grant users only the minimum permissions required to perform their tasks.
- Separate platform and service roles appropriately.
- Review access regularly to ensure permissions remain appropriate as roles change.



