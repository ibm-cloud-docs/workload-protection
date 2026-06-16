---

copyright:
  years:  2026
lastupdated: "2026-06-16"

keywords: context-based restrictions, App Configuration, network zone, and IAM

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are context-based restrictions blocking access to Workload Protection or CSPM data collection?
{: #ts-cbr}
{: troubleshoot}

After you configure context-based restrictions, you cannot access the {{site.data.keyword.sysdigsecure_short}} UI or API, or CSPM stops collecting {{site.data.keyword.cloud_notm}} resource data.
{: tsSymptoms}

Context-based restrictions rules can block access for one of the following reasons:
{: tsCauses}

- A context-based restrictions rule is restricting access to the {{site.data.keyword.sysdigsecure_short}} service from your current network context (for example, your IP address or VPC is not in the allowed network zone).
- A context-based restrictions rule is restricting access to the IBM {{site.data.keyword.appconfig_short}} instance that {{site.data.keyword.sysdigsecure_short}} uses for CSPM data collection. Because context-based restrictions rules can apply to App Configuration independently, a rule that blocks the {{site.data.keyword.sysdigsecure_short}} service from accessing {{site.data.keyword.appconfig_short}} will stop CSPM resource collection.
- A user must have the Administrator role on the {{site.data.keyword.sysdigsecure_full}} service to create, update, or delete rules. A user must also have either the **Editor** or **Administrator** role on the Context-based restrictions service to create, update, or delete network zones. A user with the Viewer role on the context-based restrictions service can only add network zones to a rule.
- Context-based restrictions do not affect connectivity of {{site.data.keyword.sysdigsecure_full}} agents since they do not use {{site.data.keyword.iamlong}}.

To resolve this issue, complete the following steps:
{: tsResolve}

1. Review the context-based restrictions rules applied to your {{site.data.keyword.sysdigsecure_short}} instance. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Context-based restrictions** and check the rules for the `sysdig-secure` service.

2. Confirm that your current network context (IP address, VPC, or service reference) is included in the network zone that is associated with the CBR rule that applies to {{site.data.keyword.sysdigsecure_short}}.

3. If CSPM data collection has stopped, check whether a context-based restrictions rule is restricting access to the IBM {{site.data.keyword.appconfig_short}} instance used by {{site.data.keyword.sysdigsecure_short}}. Add the {{site.data.keyword.sysdigsecure_short}} service as an allowed context in the {{site.data.keyword.appconfig_short}} context-based restrictions rule.

4. Confirm that the IAM identity managing context-based restrictions rules has the **Administrator** or **Editor** platform role on the {{site.data.keyword.sysdigsecure_short}} service.

For more information, see [Protecting {{site.data.keyword.sysdigsecure_short}} resources with context-based restrictions](/docs/workload-protection?topic=workload-protection-cbr).
