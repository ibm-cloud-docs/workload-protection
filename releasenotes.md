---

copyright:
  years:  2023, 2024
lastupdated: "2024-04-18"

keywords:  release notes, IBM Cloud

subcollection: workload-protection

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.sysdigsecure_full_notm}}
{: #release-notes}

Use these release notes to learn about updates to {{site.data.keyword.sysdigsecure_full}}.
{: shortdesc}

## July 2024
{: #workload-protection-july24}

### 8 July 2024
{: #workload-protection-july0824}
{: release-note}

{{site.data.keyword.sysdigsecure_full}} now supports Cloud Security Posture Management (CSPM) for {{site.data.keyword.cloud_notm}} resources with the {{site.data.keyword.cloud_notm}} Framework for Financial Services, Digital Operational Resilience Act (DORA), CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark, PCI, and many other industrial related or best practices standards.

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
