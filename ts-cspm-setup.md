---

copyright:
  years:  2026
lastupdated: "2026-05-18"

keywords: cspm, App Configuration, and trusted profile

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my {{site.data.keyword.cloud_notm}} account not showing as Active after CSPM setup?
{: #ts-cspm-setup}
{: troubleshoot}

After connecting your {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.sysdigsecure_short}} with CSPM enabled, the account connection status isn't `Active`, or no {{site.data.keyword.cloud_notm}} resources appear on the **Inventory** page.
{: tsSymptoms}

The CSPM connection might not be active for one of the following reasons:
{: tsCauses}

- The trusted profile was not created correctly, or the {{site.data.keyword.sysdigsecure_short}} service instance is not listed as a trusted entity in the profile.
- The IBM {{site.data.keyword.appconfig_short}} instance was not linked to the {{site.data.keyword.sysdigsecure_short}} instance by using the correct CLI commands.
- The IAM trusted profile does not have the required access policies to read resources across the account.
- A context-based restriction rule is blocking the {{site.data.keyword.sysdigsecure_short}} service from accessing the {{site.data.keyword.appconfig_short}} instance or other {{site.data.keyword.cloud_notm}} resources.
- For enterprise accounts, the enterprise trusted profile was not configured, or the child account trusted profiles were not set up correctly.

To resolve this issue, complete the following steps:
{: tsResolve}

1. Confirm that the trusted profile includes the {{site.data.keyword.sysdigsecure_short}} service instance as a trusted entity and that the profile has the required IAM access policies. For the required policies, see [Configuring CSPM for {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-cspm-implement).

2. Verify that the {{site.data.keyword.appconfig_short}} instance is correctly linked by running the following CLI command:

   ```sh
   ibmcloud sysdig cspm-config get --instance-id <INSTANCE_ID>
   ```
   {: pre}

   If the configuration is missing or incorrect, rerun the setup commands from the CSPM onboarding documentation.

3. Check whether any context-based restriction rules are restricting access to the {{site.data.keyword.appconfig_short}} instance. Context-based restriction rules that restrict access to {{site.data.keyword.appconfig_short}} can prevent {{site.data.keyword.sysdigsecure_short}} from collecting resource data. For more information, see [Protecting {{site.data.keyword.sysdigsecure_short}} resources with context-based restrictions](/docs/workload-protection?topic=workload-protection-cbr).

4. For enterprise accounts, confirm that the enterprise-level trusted profile and all child account trusted profiles are configured. Each child account requires its own trusted profile that grants the {{site.data.keyword.sysdigsecure_short}} service access to resources in that account.

5. After making corrections, allow up to 10 minutes for the connection status to update in the {{site.data.keyword.sysdigsecure_short}} UI.

For more information, see [Configuring CSPM for {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-cspm-implement).
