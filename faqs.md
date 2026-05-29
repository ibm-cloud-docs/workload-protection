---

copyright:
  years: 2026
lastupdated: "2026-05-29"

keywords: workload protection faq, security faq, cspm faq, agent faq, compliance faq

subcollection: workload-protection

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for {{site.data.keyword.sysdigsecure_short}}
{: #workload-protection-faq}

Frequently asked questions about {{site.data.keyword.sysdigsecure_full_notm}}.
{: shortdesc}

## What is the difference between the Free Trial and Graduated Tier plans?
{: #faq-pricing-plans}
{: faq}

The Free Trial plan gives you access to all {{site.data.keyword.sysdigsecure_short}} capabilities for 30 days at no cost. After 30 days, you can upgrade to the Graduated Tier plan, which is the paid plan. For more information, go to [Pricing](/docs/workload-protection?topic=workload-protection-pricing).

## How is pricing calculated for {{site.data.keyword.sysdigsecure_short}}?
{: #faq-pricing-calculation}
{: faq}

Your pricing depends on how you use {{site.data.keyword.sysdigsecure_short}}:

- Cloud Security Posture Management (CSPM) for cloud compliance: Priced per instance of cloud accounts being scanned
- Kubernetes protection with agents installed on clusters: Priced per worker node hour
- Host protection with agents installed on virtual machines: Priced per virtual machine (VM) node hour

Pricing is calculated monthly or hourly according to your consumption. As your usage grows, you can benefit from volume discounts across pricing tiers. For more information, go to [Pricing](/docs/workload-protection?topic=workload-protection-pricing).

## Can I use {{site.data.keyword.terraform-provider_short}} to automate {{site.data.keyword.sysdigsecure_short}} provisioning?
{: #faq-terraform-automation}
{: faq}

Yes. The [{{site.data.keyword.sysdigsecure_short}} module](https://registry.terraform.io/modules/terraform-ibm-modules/scc-workload-protection/ibm/latest){: external} provides a curated {{site.data.keyword.terraform-provider_short}} configuration for provisioning and managing {{site.data.keyword.sysdigsecure_full_notm}} instances as code. You can use it to automate instance setup consistently across accounts or environments. For an overview of available {{site.data.keyword.cloud_notm}} {{site.data.keyword.terraform-provider_short}} modules, see [About {{site.data.keyword.terraform-provider_short}} IBM Modules](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about-tim).

## Do I need separate agents if I use both {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.mon_short}} on the same cluster?
{: #faq-shared-agent}
{: faq}

No. A single agent can collect data for both {{site.data.keyword.sysdigsecure_short}} (security) and {{site.data.keyword.mon_short}} (monitoring) if you connect your instances during instance creation. For more information, go to [frequently asked questions about {{site.data.keyword.monitoringlong_notm}}](/docs/monitoring?topic=monitoring-faq#faq_4).

## Which operating systems and platforms does the {{site.data.keyword.sysdigsecure_short}} agent support?
{: #faq-agent-platforms}
{: faq}

The agent supports Kubernetes clusters ({{site.data.keyword.containershort}}, ROKS), {{site.data.keyword.redhat_openshift_notm}} clusters, {{site.data.keyword.satelliteshort}} clusters, Linux hosts (Debian, Ubuntu, CentOS, RHEL, Fedora, Amazon Linux), Windows servers, AIX hosts on {{site.data.keyword.powerSys_notm}}, and Linux hosts on {{site.data.keyword.powerSys_notm}}.

You can also deploy the agent on Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters that run outside {{site.data.keyword.cloud_notm}}, including on other cloud providers or on-premises. For deployment instructions, go to [Managing the agent](/docs/workload-protection?topic=workload-protection-agent-deploy-openshift-helm).

## What network ports does the {{site.data.keyword.sysdigsecure_short}} agent require?
{: #faq-agent-ports}
{: faq}

The agent requires outbound TCP traffic to the collector endpoint on port `6443` and to the API endpoint on port `443`. Both ports must be open for outbound traffic from your cluster or host to the {{site.data.keyword.sysdigsecure_short}} service endpoints. This applies to both public and private endpoint connections, including connections by using Virtual Private Endpoint (VPE). For a list of endpoints, go to [Endpoints](/docs/workload-protection?topic=workload-protection-endpoints).

## What Helm version is required to deploy the {{site.data.keyword.sysdigsecure_short}} agent?
{: #faq-helm-version}
{: faq}

Helm 3.6 or later is required to deploy the {{site.data.keyword.sysdigsecure_short}} agent with a Helm chart on Kubernetes, {{site.data.keyword.redhat_openshift_notm}}, or {{site.data.keyword.satelliteshort}} clusters.

## What features are available for different containers and hosts?
{: #faq-platform-features}
{: faq}

{{site.data.keyword.sysdigsecure_short}} provides the following security capabilities based on where you deploy the agent:

| Environment | Threat detection and response | Posture management | Host scanning |
|----------|-------------------------------|-------------------|---------------|
| Kubernetes clusters | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) |
| {{site.data.keyword.redhat_openshift_notm}} clusters | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) |
| {{site.data.keyword.satelliteshort}} clusters | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) |
| Linux hosts | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) |
| Windows servers | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) |
| Linux hosts on {{site.data.keyword.powerSys_notm}} | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) | ![Checkmark icon](/images/checkmark-icon.svg) |
| AIX hosts on {{site.data.keyword.powerSys_notm}} |  | ![Checkmark icon](/images/checkmark-icon.svg) |  |
{: caption="Feature availability by environment" caption-side="bottom"}

Threat detection and response
:   Identifies threats based on application, network, and host activity.

Posture management
:   Scans host configuration files and resources for compliance against benchmarks such as CIS benchmarks.

Host scanning
:   Detects vulnerabilities and identifies resolution priority.

For deployment instructions, go to the agent deployment documentation for [Kubernetes](/docs/workload-protection?topic=workload-protection-agent-deploy-kube-helm), [{{site.data.keyword.redhat_openshift_notm}}](/docs/workload-protection?topic=workload-protection-agent-deploy-openshift-helm), [{{site.data.keyword.satelliteshort}}](/docs/workload-protection?topic=workload-protection-agent-deploy-satellite), [Windows servers](/docs/workload-protection?topic=workload-protection-agent-deploy-windows), [Linux hosts on PowerVS](/docs/workload-protection?topic=workload-protection-agent-deploy-linux-powervs), or [AIX hosts on PowerVS](/docs/workload-protection?topic=workload-protection-agent-deploy-aix-powervs).

## How do I deploy agents to protect my workloads?
{: #faq-agent-deployment-steps}
{: faq}

The deployment process varies depending on the environment where your workloads run:

### Adding agents to containers (Kubernetes, {{site.data.keyword.redhat_openshift_notm}}, {{site.data.keyword.satelliteshort}})
{: #add-agents-to-container-environments}

To deploy agents in container environments, complete the following steps:

1. Verify that you have Helm 3.6 or later installed
2. Obtain your {{site.data.keyword.sysdigsecure_short}} access key and collector endpoint from your instance
3. Verify that outbound TCP traffic is allowed on port `6443` (collector) and port `443` (API)
4. Add the {{site.data.keyword.sysdigsecure_short}} Helm repository
5. Deploy the agent by using the Helm chart with your access key and collector endpoint
6. Verify that the agent pods are running successfully

### Adding agents to hosts (Linux, Windows, AIX on {{site.data.keyword.powerSys_notm}})
{: #add-agents-to-host-environments}

To deploy agents on host systems, complete the following steps:

1. Obtain your {{site.data.keyword.sysdigsecure_short}} access key and collector endpoint from your instance
2. Verify that outbound TCP traffic is allowed on port `6443` (collector) and port `443` (API)
3. Download the appropriate agent installer for your operating system
4. Run the installation script or command with your access key and collector endpoint
5. Verify that the agent service is running and connected

For detailed deployment instructions specific to your environment, go to the agent deployment documentation for [Kubernetes](/docs/workload-protection?topic=workload-protection-agent-deploy-kube-helm), [Red Hat OpenShift](/docs/workload-protection?topic=workload-protection-agent-deploy-openshift-helm), or [host environments](/docs/workload-protection?topic=workload-protection-agent-deploy-windows).

## Who is responsible for keeping the {{site.data.keyword.sysdigsecure_short}} agent up to date?
{: #faq-agent-updates}
{: faq}

{{site.data.keyword.IBM_notm}} provides regular updates to the agent image with new features, defect fixes, and security fixes, and documents changes in the agent release notes. You are responsible for updating the agent in your environment to keep it current as new versions are made available. You can track the new features and enhancements with these [release notes](https://docs.sysdig.com/en/release-notes/saas-sysdig-monitor-release-notes/).

## Which {{site.data.keyword.cloud_notm}} services can I scan for compliance issues?
{: #faq-cspm-supported-services}
{: faq}

You can scan a broad range of {{site.data.keyword.cloud_notm}} services for compliance issues, including {{site.data.keyword.cos_full_notm}}, {{site.data.keyword.containershort}}, {{site.data.keyword.redhat_openshift_notm}}, Virtual Private Cloud (VPC) resources, {{site.data.keyword.secrets-manager_short}}, databases like {{site.data.keyword.databases-for-elasticsearch}}, {{site.data.keyword.keymanagementserviceshort}}, {{site.data.keyword.registryshort}}, {{site.data.keyword.codeengineshort}}, {{site.data.keyword.messagehub}}, {{site.data.keyword.dl_short}}, {{site.data.keyword.tg_short}}, {{site.data.keyword.bpshort}}, {{site.data.keyword.mon_short}}, {{site.data.keyword.hscrypto}}, {{site.data.keyword.appid_short_notm}}, and more. For the complete list, go to [About {{site.data.keyword.cloud_notm}} Security Posture Management (CSPM)](/docs/workload-protection?topic=workload-protection-about).

## How does {{site.data.keyword.sysdigsecure_short}} collect my {{site.data.keyword.cloud_notm}} resource configurations for compliance scanning?
{: #faq-cspm-app-config}
{: faq}

{{site.data.keyword.sysdigsecure_short}} uses the aggregator feature of {{site.data.keyword.appconfig_short}} to gather your resource configuration details for compliance scanning. The aggregator feature is free and included in the Basic plan of {{site.data.keyword.appconfig_short}}. The integration uses {{site.data.keyword.IBM_notm}} {{site.data.keyword.iamshort}} trusted profiles to manage permissions. For more information, go to [Implementing CSPM for {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-cspm-implement).

## How long does it take to view compliance scan results after I connect my {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.sysdigsecure_short}}?
{: #faq-cspm-results-latency}
{: faq}

Results are typically displayed 5-10 minutes after the connection is established, depending on the number of resources in your account.

## Can I use {{site.data.keyword.sysdigsecure_short}} to scan my {{site.data.keyword.cloud_notm}} enterprise for compliance?
{: #faq-cspm-enterprise}
{: faq}

Yes. You can integrate your {{site.data.keyword.cloud_notm}} enterprise account to scan for compliance across all accounts in your organization. For more information, go to [Implementing CSPM for {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-cspm-implement) and [Setting up {{site.data.keyword.sysdigsecure_short}} to scan an enterprise for compliance](/docs/workload-protection?topic=workload-protection-cspm-tutorial-enterprise).

## How do I set up my enterprise account to work with {{site.data.keyword.sysdigsecure_short}}?
{: #faq-enterprise-setup}
{: faq}

To enable {{site.data.keyword.sysdigsecure_short}} to scan all child accounts in your enterprise, you must set up trusted profile templates and trusted profiles in your enterprise account. Without this configuration, {{site.data.keyword.appconfig_short}} cannot scan child accounts, and compliance data is collected from the enterprise account only.

Complete the following steps:

1. Create a trusted profile template with the following access policies: Viewer and ConfigReader for All Account Management services, and Reader, Viewer, and ConfigReader for All Identity and Access enabled services.
2. Assign the trusted profile template to your child accounts and account groups in the enterprise.
3. Create a trusted profile to grant {{site.data.keyword.appconfig_short}} access to read the trusted profile template with the following access policies: Viewer role on the Enterprise service, and Template Administrator, Assignment Administrator, and Viewer roles for All IAM Account Management services.
4. Configure the configuration aggregator in your {{site.data.keyword.appconfig_short}} instance with your enterprise ID, trusted profile template ID, and trusted profile ID.

For detailed step-by-step instructions, go to [Setting up {{site.data.keyword.sysdigsecure_short}} to scan an enterprise for compliance](/docs/workload-protection?topic=workload-protection-cspm-tutorial-enterprise). For best practices, go to [Best practices for enterprise accounts](/docs/workload-protection?topic=workload-protection-bp#bp-enterprise).

## Is CSPM data collection affected if I enable context-based restrictions on my {{site.data.keyword.cloud_notm}} resources?
{: #faq-cspm-cbr}
{: faq}

Yes. When context-based restrictions are enabled for any resource in your {{site.data.keyword.cloud_notm}} account, configuration data cannot be collected unless access to that resource is explicitly provided. To provide access, you need to create a rule. When asked to add a context, create a network zone and select {{site.data.keyword.appconfig_short}} as the reference service. For more information, go to [Implementing CSPM for {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-cspm-implement).

## How often does {{site.data.keyword.sysdigsecure_short}} scan my {{site.data.keyword.cloud_notm}} resources for compliance?
{: #faq-scan-frequency}
{: faq}

{{site.data.keyword.sysdigsecure_short}} automatically scans all connected {{site.data.keyword.cloud_notm}} accounts every 24 hours based on the compliance policies that you applied. The 24-hour schedule begins when you connect an account for the first time. You can also have scans on demand at no additional charge.

Compliance violations are displayed on the **Compliance** page in the {{site.data.keyword.sysdigsecure_short}} UI. A compliance snapshot is also available from **Security** > **Overview** in {{site.data.keyword.cloud_notm}} console.

## Can I accept a compliance risk without remediating it?
{: #faq-risk-acceptance}
{: faq}

Yes. For any failing control, you can accept the risk either temporarily (with an expiration date) or permanently. You can accept risk at the individual resource level or globally for all the resources that are associated with a specific control. Accepted risks are tracked and visible in the compliance overview. For more information, go to [Analyzing compliance postures from detection to remediation](/docs/workload-protection?topic=workload-protection-compliance).

## Can I create custom posture policies and controls?
{: #faq-custom-policies}
{: faq}

Yes. You can create custom posture policies from scratch or by starting from an existing predefined policy as a template. You can also create custom controls and customize control parameters to tailor compliance evaluation to your organization's specific requirements. For more information, go to [Creating a custom policy](/docs/workload-protection?topic=workload-protection-posture-policy-create) and [Creating custom controls](/docs/workload-protection?topic=workload-protection-custom-controls).

## Who is responsible for managing custom threat detection rules and policies?
{: #faq-custom-rules-responsibility}
{: faq}

You are responsible for updating your custom policies and tracking changes to them through your own change management process. {{site.data.keyword.IBM_notm}} updates the default rules and policies as requirements change. For more information, go to [Understanding your responsibilities](/docs/workload-protection?topic=workload-protection-shared-responsibilities).

## What access do users need to use {{site.data.keyword.sysdigsecure_short}}?
{: #faq-user-access}
{: faq}

Users need both platform and service roles to work with {{site.data.keyword.sysdigsecure_short}}:

Platform roles
:   Control access to manage instances in {{site.data.keyword.cloud_notm}}. Users need at  the Viewer role to view instances the Administrator or Editor role to create or delete instances.

Service roles
:   Define permissions within the {{site.data.keyword.sysdigsecure_short}} UI. The Manager role provides full access including managing access keys, teams, and agents. The Writer role allows creating and editing content, managing policies, and viewing reports. The Reader role provides view-only access to events, reports, and policies.

A user with an Administrator platform role automatically has the Manager service role permissions. For detailed information about roles and permissions, go to [Controlling access through IAM](/docs/workload-protection?topic=workload-protection-iam).

## What are the predefined policies that I can use with {{site.data.keyword.sysdigsecure_short}}?
{: #faq-predefined-policies}
{: faq}

{{site.data.keyword.sysdigsecure_short}} provides several types of predefined policies to help you secure your workloads:

Supply chain policies
:   Validate container image signatures and enforce security requirements before deployment. These policies help ensure that only trusted images run in your environment.

Threat detection policies
:   Detect runtime threats by using Falco-based rules that monitor application, network, and host activity. These policies identify suspicious behavior and security incidents as they occur.

Vulnerability management policies
:   Identify and prioritize vulnerabilities in container images and hosts. These policies help you understand which vulnerabilities pose the greatest risk and should be remediated first.

Posture policies
:   Evaluate compliance against security benchmarks and regulatory frameworks such as CIS benchmarks, PCI DSS, NIST, and {{site.data.keyword.framework-fs_full}}. These policies scan your cloud resources and workload configurations for compliance violations.

You can view and apply these policies from {{site.data.keyword.sysdigsecure_short}} under **Policies**. For more information about policy types and how to use them, go to [Policies](https://docs.sysdig.com/en/docs/sysdig-secure/policies/){: external} in the Sysdig documentation. For {{site.data.keyword.cloud_notm}}-specific posture policies, go to [Posture policies](/docs/workload-protection?topic=workload-protection-posture-policies).

## Do context-based restrictions affect {{site.data.keyword.sysdigsecure_short}} agent connectivity?
{: #faq-cbr-agents}
{: faq}

No. Context-based restrictions do not affect the connectivity of {{site.data.keyword.sysdigsecure_short}} agents because agents authenticate by using access keys rather than {{site.data.keyword.iamlong}} tokens. Agents can connect through either public or private service endpoints. For more information, go to [Protecting resources with context-based restrictions](/docs/workload-protection?topic=workload-protection-cbr).

When context-based restrictions are enabled for any resource in your {{site.data.keyword.cloud_notm}} account, compliance data cannot be collected unless access to that resource is explicitly provided.
{: note}


## What IAM roles are required to create or update context-based restriction rules for {{site.data.keyword.sysdigsecure_short}}?
{: #faq-cbr-roles}
{: faq}

A user must have the Administrator role on the {{site.data.keyword.sysdigsecure_short}} service to create, update, or delete context-based restriction rules. To create, update, or delete network zones, a user must have the Editor or Administrator role on the Context-based Restrictions service. A user with the Viewer role on the Context-based Restrictions service can only add network zones to an existing rule. For more information, go to [Protecting resources with context-based restrictions](/docs/workload-protection?topic=workload-protection-cbr).

## Does {{site.data.keyword.sysdigsecure_short}} remain available during regional outages?
{: #faq-high-availability}
{: faq}

Yes. {{site.data.keyword.sysdigsecure_short}} is a multi-tenant, regional service deployed across multizone regions (MZRs). Each region has three availability zones (data centers) for redundancy, with independent power, cooling, and network infrastructure. If one zone fails, the service continues operating from the remaining zones. The service is available in nine regions across Asia Pacific, Europe, North America, and South America. For more information, go to [High availability and disaster recovery](/docs/workload-protection?topic=workload-protection-ha-dr).

## Which actions generate audit events in {{site.data.keyword.sysdigsecure_short}}?
{: #faq-audit-events}
{: faq}

{{site.data.keyword.sysdigsecure_short}} automatically generates {{site.data.keyword.atracker_short}} audit events when the following actions occur:

- When captures are created, read, listed, updated, or deleted
- When teams are created, read, listed, updated, or deleted
- When access keys are created

These events comply with the Cloud Auditing Data Federation (CADF) standard. For more information, go to [Auditing events](/docs/workload-protection?topic=workload-protection-at_events).

## What advanced security features does {{site.data.keyword.sysdigsecure_short}} provide?
{: #faq-sysdig-features}
{: faq}

{{site.data.keyword.sysdigsecure_short}} provides comprehensive security capabilities for the workloads. Key features include:

Posture Management
:   Organize resources into zones for compliance evaluation, apply posture policies, and track compliance across your cloud infrastructure and Git repositories.

Supply Chain Security
:   Validate image signatures, enforce supply chain policies on Kubernetes clusters, and ensure that container images meet security requirements before deployment.

Runtime Protection
:   Detect threats continuously using Falco-based detection rules, tune runtime policies to reduce false positives, and automatically adjust security policies based on observed application behavior.

Incident Response
:   Use Rapid Response to connect to remote shells for investigating security events, run security tools directly from alerts, and troubleshoot incidents without separate host access.

Activity Monitoring
:   Track commands, network activity, file operations, and Kubernetes API requests with Activity Audit for forensics and investigation.

Integration
:   Forward security events to third-party SIEM platforms like Splunk, Elastic Stack, QRadar, and ArcSight for centralized security analysis.

For detailed configuration and usage of these features, go to the [Sysdig Secure documentation](https://docs.sysdig.com/en/docs/sysdig-secure/). For IBM Cloud-specific setup and integration, go to the [{{site.data.keyword.sysdigsecure_short}} documentation](/docs/workload-protection).
