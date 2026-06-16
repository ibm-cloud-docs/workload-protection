---

copyright:
  years: 2026
lastupdated: "2026-06-16"

keywords: integration errors, IAM, App Configuration, cspm, trusted profile

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my {{site.data.keyword.cloud_notm}} integration showing errors or not Active?
{: #troubleshoot-integration-errors}
{: troubleshoot}
{: support}

After connecting your {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.sysdigsecure_short}} with CSPM enabled, the **Integrations > {{site.data.keyword.cloud_notm}}** page shows your account in **Error** status with error messages, the account connection status isn't `Connected`, or no {{site.data.keyword.cloud_notm}} resources appear on the **Inventory** page.
{: tsSymptoms}

Common error messages include:
- > IBM Token api call failed with error code '500'
- > Exception while getting IBM {{site.data.keyword.appconfig_short}} Account Token
- > Failed to connect to database

The {{site.data.keyword.cloud_notm}} integration might not be active for one of the following reasons:
{: tsCauses}

- The trusted profile was not created correctly, or the {{site.data.keyword.sysdigsecure_short}} service instance is not listed as a trusted entity in the profile.
- The IAM trusted profile does not have the required access policies to read resources across the account.
- The {{site.data.keyword.appconfig_short}} instance is not accessible or is in an error state.
- A context-based restriction rule is blocking the {{site.data.keyword.sysdigsecure_short}} service from accessing the {{site.data.keyword.appconfig_short}} instance or other {{site.data.keyword.cloud_notm}} resources.
- For enterprise accounts, the enterprise trusted profile was not configured, or the child account trusted profiles were not set up correctly.
- Temporary backend issues are causing database connection errors.

To resolve this issue, complete the following steps:
{: tsResolve}

1. Verify that the {{site.data.keyword.appconfig_short}} instance exists and is accessible:
   1. In the {{site.data.keyword.cloud_notm}} console, select **Resource list** from the navigation menu.
   2. Select your {{site.data.keyword.sysdigsecure_short}} instance.
   3. Navigate to **Sources** > **{{site.data.keyword.cloud_notm}}** to verify the {{site.data.keyword.appconfig_short}} instance name.
   4. Ensure the instance is in `Active` state.

2. Confirm that the trusted profile includes the {{site.data.keyword.sysdigsecure_short}} service instance as a trusted entity and that the profile has the required IAM access policies:
   1. In the {{site.data.keyword.cloud_notm}} console, select **Manage** from the menu bar, then select **Access (IAM)**.
   2. Select **Trusted profiles** from the navigation menu.
   3. Locate the trusted profile associated with your {{site.data.keyword.sysdigsecure_short}} instance.
   4. Verify it has the necessary service-to-service authorizations.
   5. For the required policies, see [Configuring CSPM for {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-cspm-implement).

3. Check whether any context-based restrictions are limiting access to the {{site.data.keyword.appconfig_short}} instance, since these restrictions can prevent {{site.data.keyword.sysdigsecure_short}} from collecting resource data. For more information, see [Protecting {{site.data.keyword.sysdigsecure_short}} resources with context-based restrictions](/docs/workload-protection?topic=workload-protection-cbr).

4. For enterprise accounts, confirm that the enterprise-level trusted profile and all child account trusted profiles are configured. Each child account requires its own trusted profile that grants the {{site.data.keyword.sysdigsecure_short}} service access to resources in that account.

5. For database connection errors, these are typically temporary backend issues. Wait 30-60 minutes and check if the error resolves automatically.

6. After making corrections, allow up to 10 minutes for the connection status to update in the {{site.data.keyword.sysdigsecure_short}} UI.

7. If the error persists for more than 2 hours, contact {{site.data.keyword.cloud_notm}} support with:
   - Your {{site.data.keyword.sysdigsecure_short}} instance CRN
   - The complete error payload from the integration page
   - The timestamp when the error first appeared

For more information, see [Configuring CSPM for {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-cspm-implement).
