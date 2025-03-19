---

copyright:
  years:  2023, 2024
lastupdated: "2025-03-19"

keywords:  release notes, IBM Cloud

subcollection: workload-protection

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.sysdigsecure_full_notm}}
{: #release-notes}

Use these release notes to learn about updates to {{site.data.keyword.sysdigsecure_full}}.
{: shortdesc}

## March 2025
{: #workload-protection-mar25}

### 19 March 2025
{: #workload-protection-mar1925}
{: release-note}

Resource Report (CSV) is now available in {{site.data.keyword.cloud_notm}}
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
