---

copyright:
  years:  2023, 2024
lastupdated: "2025-08-22"

keywords:  release notes, IBM Cloud

subcollection: workload-protection

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.sysdigsecure_full_notm}}
{: #release-notes}

Use these release notes to learn about updates to {{site.data.keyword.sysdigsecure_full}}.
{: shortdesc}

## August 2025
{: #workload-protection-aug25}

## 4 August 2025

{{site.data.keyword.cloud_notm}} Framework for Financial Services v2.0
:   {{site.data.keyword.sysdigsecure_short}} now includes a new posture policy to continuously track compliance of Financial Services v2.0. For more information about this policy, see [the change log](/docs/workload-protection?topic=workload-protection-financial-services).

## July 2025
{: #workload-protection-july25}

## 10 July 2025
{: #workload-protection-july1025}

Now Generally Available: Admission Controller
:   {{site.data.keyword.sysdigsecure_short}} now provides a new Admission Controller, delivering powerful deploy-time security enforcement across Kubernetes environments. You can use Admission Controller to integrate Kubernetes Security Posture Management (KSPM) and Vulnerability Management (VM) into your deployment workflows. Admission Controller enables a shift-left approach by preventing risky configurations and vulnerable images from reaching production. The Admission Controller has the following features:

    * Deploy-time image scanning. Admission Controller integrates with scan policies to evaluate images at deployment time, blocking workloads that use images with CVEs, misconfigurations, or policy violations. Workloads are rejected before scheduling to a node, eliminating unnecessary risk.
    * Kubernetes audit logging. This feature enables Audit Detections to record API-level admission decisions, including who attempted deployments, when, and why actions were allowed or blocked. This provides a complete audit trail for security investigations and policy tuning. See also: [Kubernetes Audit Logging](/docs/workload-protection?topic=workload-protection-audit_logging).
    * Kubernetes posture enforcement. This feature applies posture policies to define best practices, such as preventing privileged containers, enforcing non-root users, or applying resource limits. The Admission Controller evaluates these policies during admission and blocks non-compliant deployments. You can assign different policies per zone to account for environment-specific constraints (for example, staging versus production).


## June 2025
{: #workload-protection-june25}

## 27 June 2025
{: #workload-protection-june2725}
{: release-note}

Automatically detect {{site.data.keyword.cloud_notm}} Virtual Servers for VPC that are exposed
:    {{site.data.keyword.sysdigsecure_short}} now detects Virtual Servers for VPC that are exposed as part of the Network Exposure module. This update enhances visibility for {{site.data.keyword.cloud_notm}} customers by enabling identification and analysis of publicly exposed virtual servers, closing a critical security gap in multi-cloud environments. Exposed virtual servers can be analyzed under Inventory or Search.

Threats module is now available in {{site.data.keyword.sysdigsecure_short}}
:   Threats combine related security signals into a single, actionable security incident. It provides context driven correlation, such as Kubernetes workloads or attack phases. This consolidation accelerates understanding the scope and criticaly of threats. You can automate responses such as sending notifications when a new threat is discovered by using Automations under Policies. 


## May 2025
{: #workload-protection-may25}

## 23 May 2025
{: #workload-protection-may2325}
{: release-note}

[IBM Cloud Shell settings](https://cloud.ibm.com/docs/account?topic=account-shell-settings) are now supported for {{site.data.keyword.cloud_notm}} CSPM
:   {{site.data.keyword.sysdigsecure_short}} now ingests your {{site.data.keyword.cloud_notm}} Shell settings as part of Cloud Security Posture Management (CSPM). This enhancement enables you to validate the Cloud Shell locations and features with three new posture controls or by creating custom controls for more flexibility. 

## 21 May 2025
{: #workload-protection-may2125}
{: release-note}

Automatically onboard new {{site.data.keyword.cloud_notm}} accounts for {{site.data.keyword.cloud_notm}} Enterprise
:   {{site.data.keyword.sysdigsecure_full_notm}} now automatically discovers and onboards newly created active IBM Cloud accounts, helping ensure your cloud environment is up-to-date without manual intervention. {{site.data.keyword.sysdigsecure_short}} performs this synchronization every 24 hours, onboarding new accounts and offboarding those that have been removed from your {{site.data.keyword.cloud_notm}} Enterprise. Resources associated with removed accounts will also be deleted from inventory.

## April 2025
{: #workload-protection-apr25}

## 12 April 2025
{: #workload-protection-apr1225}
{: release-note}

Updates to the {{site.data.keyword.sysdigsecure_full_notm}} infrastructure
:   {{site.data.keyword.sysdigsecure_full_notm}} is upgrading its network load balancers and service endpoints infrastructure. With this change the regional endpoints (public and private) use new virtual IP addresses. Action might be required when accessing {{site.data.keyword.sysdigsecure_full_notm}}:

    * If you use an IP address other than the URL domain name
    * If you have IP-based allowlists or firewall rules running in your environment
    * If you have IP address-specific routing

    For details on the changes and the new IP addresses, check out [Endpoints](/docs/workload-protection?topic=workload-protection-endpoints).



### 7 April 2025
{: #workload-protection-apr725}
{: release-note}

Posture for Windows Servers
:   This feature provides compliance scanning for standalone Windows Server hosts, enabling security and regulatory compliance checks for Windows environments. With this release, CIS Windows Server 2022 Benchmark v3.0.0 and CIS Windows Server 2019 Benchmark v3.0.1 Posture policies are provided. For installation, see [Managing the {{site.data.keyword.sysdigsecure_short}} agent on Windows Servers](/docs/workload-protection?topic=workload-protection-agent-deploy-windows).

Host Scanning for Windows Servers
:   This feature provides coverage for Windows Server operating system vulnerabilities sourced from [Microsoft Security Response Center](https://www.microsoft.com/en-us/msrc){: external}. In addition, the Windows {{site.data.keyword.sysdigsecure_short}} agent detects any non operating-system package vulnerabilities. A single agent supports both Posture and Host Scanning features. For installation, see [Managing the {{site.data.keyword.sysdigsecure_short}} agent on Windows Servers](/docs/workload-protection?topic=workload-protection-agent-deploy-windows).

Power Virtual Server Cloud Security Posture Management
:   {{site.data.keyword.sysdigsecure_short}} now supports PowerVS resources as part of its Cloud Security Posture Management (CSPM) feature. Supported resources includes PowerVS Workspaces, Instances, Instance Volumnes, Networks, Network Security Groups and Public Networks. Any existing {{site.data.keyword.sysdigsecure_short}} with {{site.data.keyword.cloud_notm}} CSPM enabled will automatically begin collecting PowerVS resources.

## March 2025
{: #workload-protection-mar25}

### 27 March 2025
{: #workload-protection-mar2725}
{: release-note}

Tenant-Aware Hierarchical Posture Scanning
:   {{site.data.keyword.cloud_notm}} is introducing Tenant-Aware Hierarchical Posture Scanning, a new capability designed to streamline posture management in multi-tenant environments. This feature allows parent tenants to seamlessly integrate posture scanning results from child tenants, ensuring consistent policy application and reporting while eliminating the need for complex cross-region data transfers. To activate the Tenant-Aware Hierarchical Posture Scanning feature, customers must contact {{site.data.keyword.cloud_notm}} Support. Our team will assist with enabling the feature and guiding you through the setup process to ensure smooth integration into your environment.

In-Use for Linux Hosts is now available in {{site.data.keyword.cloud_notm}}
:   Starting with {{site.data.keyword.cloud_notm}} Linux v13.8.0, you can recognize In-Use Packages on hosts. This addition extends {{site.data.keyword.cloud_notm}} coverage and helps reduce scope of vulnerabilities you should care about first for remediation; further reducing noise in an ever expanding VM landscape.

### 19 March 2025
{: #workload-protection-mar1925}
{: release-note}

Resource Report (CSV) is now available in {{site.data.keyword.sysdigsecure_short}}
:   Resource Report generates a CSV that includes Compliance results with the resource details: Name, CRN, Control status, remediation, posture policy, resource labels and many more details. Scope the report to the policy you prefer: Financial Services framework, CIS Benchmark for IBM Cloud or Kubernetes, DORA or PCI that you can schedule daily, weekly or monthly. Start today by accessing your {{site.data.keyword.sysdigsecure_short}} UI and navigating to the **Reporting** page and selecting **New Schedule**.

## February 2025
{: #workload-protection-feb25}

### 26 February 2025
{: #workload-protection-feb2625}
{: release-note}

Deprecation of v1beta1 APIs for Scanning Engine
:   As of 25 February 2025, the following APIs are deprecated:

- /secure/vulnerability/v1beta1/runtime-results
- /secure/vulnerability/v1beta1/registry-results
- /secure/vulnerability/v1beta1/pipeline-results
- /secure/vulnerability/v1beta1/results/<result-id>

The API v1 enhances consistency and alignment with platform API standards, and offers improved response schema:

- /secure/vulnerability/v1/runtime-results
- /secure/vulnerability/v1beta1/registry-results
- /secure/vulnerability/v1/pipeline-results
- /secure/vulnerability/v1/results/<result-id>

If you are currently working with v1beta1 APIs, you must migrate to the new APIs by 1 September, 2025.

### 18 February 2025
{: #workload-protection-feb1825}
{: release-note}

Custom Risks for {{site.data.keyword.cloud_notm}}
:   Custom Risks empowers your security team to tackle unique security challenges by defining, writing, and executing custom risk patterns. Create adaptive queries tailored to your specific environment and risk tolerance, then build graph queries and save them as Custom Risks for ongoing management. Start today by accessing your {{site.data.keyword.sysdigsecure_short}} UI and navigating to the **Risks** page and selecting **Custom Risks**.

Graph Search for {{site.data.keyword.cloud_notm}}
:   This feature lets you explore and access data on GraphDB by querying entities and relationships with SysQL, including all {{site.data.keyword.cloud_notm}} findings. The intuitive query builder ensures a seamless experience and lets you proactively identify risky patterns before they escalate into full-fledged threats. Start today by accessing your {{site.data.keyword.sysdigsecure_short}} UI and navigating to the **Inventory** page and selecting **Search**.

Posture management for Oracle Cloud Infrastructure (OCI)
:   {{site.data.keyword.sysdigsecure_short}} now provides out-of-the-box posture policies and controls for Oracle Cloud Infrastructure (OCI), including graph-based security analytics and custom risks. 

### 13 February 2025
{: #workload-protection-feb25}
{: release-note}

Information Technology Security Guidance (ITSG-33) now available in {{site.data.keyword.sysdigsecure_short}}
:   {{site.data.keyword.sysdigsecure_short}} now provides an out-of-the-box policy and controls for Information Technology Security Guidance (ITSG-33). This policy can be leveraged to manage the overall posture for hybrid multicloud environments including {{site.data.keyword.cloud_notm}}, AWS, Azure, GCP, Kubernetes and Linux.

## January 2025
{: #workload-protection-jan25}

### 13 January 2025
{: #workload-protection-jan25}
{: release-note}

Posture Management for AIX servers on PowerVS
:   SCC Workload Protection now provides posture compliance for AIX operating system, including multiple out-of-the-box policies
For more information, check out [Managing the Workload Protection agent in AIX on PowerVS](/docs/workload-protection?topic=workload-protection-agent-deploy-aix-powervs).

Compliance Readiness Report
:   You can generate a PDF of the Compliance Readiness Report, providing an overview of the current state of a compliance policy. The report highlights the status of passing requirements and controls, along with the count of passing and failing resources for each control.

Malware Control Policy
:   SCC Workload Protection is releasing a new Runtime Threat Policy for Malware Detection.
You can now detect Malware being executed in your environment by detecting the known malware hashes and utilize YARA rules to enhance the detection capabilities. 
Create a new **Malware Control Policy** under Policies > Runtime Policies.

## October 2024
{: #workload-protection-oct24}

### 10 October 2024
{: #workload-protection-oct1024}
{: release-note}

Now Generally Available: Posture Management for IBM Cloud in SCC Workload Protection
:   SCC Workload Protection now provides posture management (CSPM) for IBM Cloud resources with regulatory and industry leading out-of-the-box policies, a unified compliance posture dashboard with detailed remediation guidance and a comprehensive view of assets across hybrid multicloud.

For more information, check out [About IBM Cloud Security Posture Management (CSPM)](/docs/workload-protection?topic=workload-protection-about).

## September 2024
{: #workload-protection-sep24}

### 30 September 2024
{: #workload-protection-sep3024}
{: release-note}

Full custom controls for CSPM
:   You can now create Custom Controls for CSPM via Terraform. Define your REGO code, remediation playbooks and severity from scratch to meet your compliance requirements

Package Deny List for Vulnerability rules
:   The new Package Deny list vulnerability rule lets you control which packages are allowed in your codebase.
    By defining these rules, you can enforce stricter security measures and maintain tighter control over your software artifacts.

New Posture Policies
:   {{site.data.keyword.sysdigsecure_short}} now includes Posture Policies for Bottlerocket, Rocky Linux 9, Ubuntu 20, Ubuntu 22, RHEL 8, and RHEL 9.
    These new policies are designed to help you maintain security compliance across a broader range of Linux distributions.

## August 2024
{: #workload-protection-aug24}

### 20 August 2024
{: #workload-protection-aug2024}
{: release-note}

Identify Network Exposure in Inventory
:   The new added Network Exposure tab in Inventory shows the reason and how resources are exposed. It supports Hosts and Workloads.

Resource Packages in Inventory
:   You can now use the Packages module in Inventory to track the vulnerabilities and the analyzed packages of your images.

    In addition, you can filter by Package to find all workloads with a specific package in your environment.

:   Layered Analysis
{{site.data.keyword.sysdigsecure_short}} now analyzes the image hierarchy exposing the layer each vulnerability has been identified or from which packages introduce each layer.
Better ownership and remediation details are included now by differentiating the base image and application layers and including a new set of recommendations to fix the major issues identified in the image.

## July 2024
{: #workload-protection-july24}

### 8 July 2024
{: #workload-protection-july0824}
{: release-note}

{{site.data.keyword.sysdigsecure_full}} now supports Cloud Security Posture Management (CSPM) for {{site.data.keyword.cloud_notm}} resources with the {{site.data.keyword.cloud_notm}} Framework for Financial Services, Digital Operational Resilience Act (DORA), CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark, PCI, and many other industry related or best practices standards.

## April 2024
{: #workload-protection-apr24}

### 16 April 2024
{: #workload-protection-apr1624}
{: release-note}

{{site.data.keyword.sysdigsecure_short}} announces support for [Risks](/docs/workload-protection?topic=workload-protection-risks), a module that consolidates all findings from your multi-cloud environment and includes an attack path analysis to help you prioritize the major detected risks.

### 29 April 2024
{: #workload-protection-apr2924}
{: release-note}

{{site.data.keyword.sysdigsecure_short}} announces support for [Managing the Workload Protection agent in Linux on PowerVS](/docs/workload-protection?topic=workload-protection-agent-deploy-linux-powervs).

## February 2024
{: #workload-protection-feb24}

### 8 February 2024
{: #workload-protection-feb0824}
{: release-note}

{{site.data.keyword.sysdigsecure_short}} announces the ability to [deploy and manage an agent on Satellite using a Helm chart](/docs/workload-protection?topic=workload-protection-agent-deploy-satellite).

### 20 February 2024
{: #workload-protection-feb2024}
{: release-note}

{{site.data.keyword.sysdigsecure_short}} announces support for [Inventory](/docs/workload-protection?topic=workload-protection-inventory), a detailed view of all your resources across your multi-cloud environments (AWS, Azure and Google Public Cloud), Kubernetes environments (such as IKS, ROKS, or any other Kubernetes platform) as well as your container images.

## January 2024
{: #workload-protection-jan24}

### 18 January 2024
{: #workload-protection-jan1624}
{: release-note}

Deprecation of Sysdig Secure + Monitor plan in IBM Cloud Monitoring
: As of 18 January 2024, the Graduated Tier - Sysdig Secure + Monitor plan in IBM Cloud Monitoring is deprecated. For current Workload Protection users, there is no change to functionality. However, if you are currently working with the Sysdig Secure through IBM Cloud Monitoring, you must move to a Workload Protection based plan by the 18 August 2024 to maintain the same functionality. For more information about the transition see [the frequently asked questions](/docs/monitoring?topic=monitoring-faq#faq_4).

Deprecation of version 1 of the scanning engine
:   As of 18 January 2024, Version 1 of the scanning engine in Workload Protection is deprecated. The functionality is replaced by a new scanning engine with better performance and more capabilities. Any new instances that are created starting today are automically configured to use the new engine. If you are currently working with an existing instance, you must migrate to the new engine by 18 January, 2025. When you migrate, you must also move from the legacy node-analyzer to the new one. In some cases, uninstalling and reinstalling by using Helm is the simplest approach. If you are working with a pipeline or registry scanning, you will need to start using the new scanning components. [Learn more about scanning engines](https://docs.sysdig.com/en/docs/sysdig-secure/scanning/new-scanning-engine/){: external}.

## September 2023
{: #workload-protection-sep23}

### 18 September 2023
{: #workload-protection-sep1823}
{: release-note}

New vulnerability scanning engine available
:   {{site.data.keyword.sysdigsecure_short}} announces the new vulnerability scanning engine is now available.

## May 2023
{: #workload-protection-may23}

### 10 May 2023
{: #workload-protection-may1023}
{: release-note}

Availability in additional regions
:   {{site.data.keyword.sysdigsecure_short}} is available for use in [multiple regions.](/docs/workload-protection?topic=workload-protection-regions)

## April 2023
{: #workload-protection-apr23}

### 14 April 2023
{: #workload-protection-apr1423}
{: release-note}

Limited availability
:   {{site.data.keyword.sysdigsecure_short}} is available for limited use in the `us-east` region.
