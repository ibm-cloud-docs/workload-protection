---

copyright:
  years:  2023, 2026
lastupdated: "2026-06-18"

keywords: container security, host security, compliance, agent-based protection

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# About {{site.data.keyword.sysdigsecure_short}}
{: #about}

{{site.data.keyword.sysdigsecure_full}} is a cloud-native application protection platform (CNAPP) that helps secure workloads across hybrid multicloud and on-premises environments, including AI workloads. You can identify vulnerabilities, validate configurations, permissions, and compliance, detect and block runtime threats, and respond to incidents. {{site.data.keyword.sysdigsecure_short}} supports diverse platforms, including cloud, on-premises infrastructure, hosts, virtual machines, and container environments.
{: shortdesc}

{{site.data.keyword.sysdigsecure_short}} uses functionality from Sysdig Secure. You might see links to [Sysdig Secure documentation](https://docs.sysdig.com/en/docs/sysdig-secure/){: external} throughout this content because that information also applies to {{site.data.keyword.sysdigsecure_short}}.
{: note}

{{site.data.keyword.sysdigsecure_short}} supports your {{site.data.keyword.cloud_notm}} account and resources in two main ways:

Cloud security posture management (CSPM)
:   Assesses and monitors compliance by validating configurations, resource settings, and identity permissions against frameworks such as the {{site.data.keyword.framework-fs_full}}.

Cloud workload protection platform (CWPP) with agent-based protection
:   Extends protection into your workloads by using agents to detect vulnerabilities, monitor activity, and respond to threats during runtime.

Together, these capabilities provide consistent visibility and protection across hybrid multicloud and on-premises environments, including AI workloads, from configuration and compliance validation to runtime security.

## Managing compliance with CSPM
{: #use-cases-cspm}

CSPM provides a unified platform to manage the security and compliance of applications, workloads, and infrastructure that run on {{site.data.keyword.cloud_notm}}, in other clouds, and on-premises.

{{site.data.keyword.sysdigsecure_short}} supports multiple cloud providers, such as AWS and Azure, in addition to {{site.data.keyword.cloud_notm}}. For more information, see [Connect cloud accounts](https://docs.sysdig.com/en/sysdig-secure/connect-cloud-accounts/){: external}.
{: tip}

App Configuration connection
:   To enable CSPM with {{site.data.keyword.sysdigsecure_short}}, your {{site.data.keyword.cloud_notm}} account needs an instance of {{site.data.keyword.appconfig_short}}. {{site.data.keyword.appconfig_short}} uses a configuration aggregator to gather configuration information in your {{site.data.keyword.cloud_notm}} account, which allows {{site.data.keyword.sysdigsecure_short}} to access your resources and scan them for compliance.

    By default, {{site.data.keyword.sysdigsecure_short}} is CSPM-enabled. However, if you disable CSPM before provisioning {{site.data.keyword.sysdigsecure_short}}, or if you want to use an existing instance of {{site.data.keyword.appconfig_short}}, you can [set up the connection manually](/docs/workload-protection?topic=workload-protection-cspm-tutorial-enterprise#connect-appconfig).
    {: note}

Compliance frameworks
:   [Default frameworks are available for immediate use](/docs/workload-protection?topic=workload-protection-posture-policies-services), such as DORA, NIST, and the {{site.data.keyword.framework-fs_notm}}. With these predefined policies, you can implement and validate the controls that are required to meet industry standards and regulations. {{site.data.keyword.sysdigsecure_short}} runs automated configuration checks and provides audit-ready reports at both the infrastructure and application levels. For more information, see [Analyzing compliance postures from detection to remediation](/docs/workload-protection?topic=workload-protection-compliance).

Policy management
:   You can create and manage your own custom policies to ensure that your workloads are compliant with your organization's policies. For example, you can create a policy to ensure that your workloads are running in a specific region or that they're using a specific version of a database. You can also create policies to ensure that your workloads are using specific security features, such as encryption or multi-factor authentication. For more information, see [creating a custom policy](https://docs.sysdig.com/en/sysdig-secure/manage_posture_policies/#create-a-custom-policy){: external}.

Addressing failures
:   When a control fails, detailed remediation instructions are provided to address the failure. {{site.data.keyword.sysdigsecure_short}} also provides a risk acceptance flow for failed controls with options to include the reason for accepting the risk and an expiration date for the acceptance. You can accept risk at one resource level or globally for all resources from one control. For more information, see [risks](https://docs.sysdig.com/en/sysdig-secure/risks/){: external}.

## Securing containers and hosts with agents
{: #use-cases-agents}

For an additional layer of security, add an agent to your containers and hosts to gain visibility into your workloads. {{site.data.keyword.sysdigsecure_short}} uses Server Endpoint Detection and Response (EDR) capabilities to provide comprehensive runtime protection and threat detection.

Server endpoint detection and response (EDR)
:   {{site.data.keyword.sysdigsecure_short}} instruments hosts, VMs, and Kubernetes or {{site.data.keyword.openshiftshort}} clusters through eBPF technology to inspect all system activity through system calls with minimal performance impact. This deep visibility allows you to detect and respond to threats in real time across your entire infrastructure.

Threat detection and response
:   With thousands of out-of-the-box policies that are updated weekly by the Sysdig Threat Research team, you get immediate protection against the latest threats. You can customize existing rules or create new ones using the Falco language, the open source cloud-native standard for runtime security. Beyond rule-based detection, behavioral analysis helps identify common threats like crypto mining activities, while workload profiling automatically defines expected behavior to extend your detection capabilities. For more information, see [Threats](https://docs.sysdig.com/en/sysdig-secure/threats/){: external}.

Proactive threat prevention
:   {{site.data.keyword.sysdigsecure_short}} goes beyond detection by offering preemptive blocking capabilities. You can prevent blacklisted or malicious binaries from executing, including identified malware or drifted binaries in a container image. Advanced remediation features allow you to automatically execute corrective actions such as killing processes, killing or pausing containers, and more.

File Integrity Monitoring (FIM)
:   Define detection rules per scope (path, filename, command, user, and more) to detect all possible file activities at the source, including reading files, writing files, writing directories, and other operations. This helps you maintain the integrity of critical system files and detect unauthorized changes.

Policies for your lifecycle
:   Supply chain policies, threat detection policies, and network security policies work together to provide comprehensive security of your containers and hosts. [Supply chain policies](https://docs.sysdig.com/en/docs/sysdig-secure/policies/supply_chain/){: external} help ensure only trusted code enters your environment, [threat detection policies](https://docs.sysdig.com/en/sysdig-secure/threat-detection-policies/){: external} monitor for malicious behavior during runtime, and [network security policies](https://docs.sysdig.com/en/sysdig-secure/network/){: external} control how workloads communicate with each other.

Kubernetes Security Posture Management (KSPM)
:   {{site.data.keyword.sysdigsecure_short}} offers visibility into your Kubernetes clusters, helping you monitor configurations, enforce security policies, and detect misconfigurations or violations of best practices. For more information, see [Compliance](https://docs.sysdig.com/en/sysdig-secure/compliance/){: external}.
