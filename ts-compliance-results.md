---

copyright:
  years: 2026
lastupdated: "2026-05-20"

keywords: compliance results,

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are my compliance scan results not showing?
{: #ts-compliance-results}
{: troubleshoot}
{: support}

You have attached a policy to a zone, but no compliance results appear on the **Compliance** page, or the page shows "0 items evaluated" for all controls.
{: tsSymptoms}

This can occur due to several reasons:
{: tsCauses}

- The cloud scan has not completed yet.
- The {{site.data.keyword.cloud_notm}} integration is not properly configured.
- The {{site.data.keyword.appconfig_short}} instance or trusted profile was not created correctly.
- There are no resources in the zone that match the policy requirements.
- The scan failed due to backend errors.

To resolve this issue:
{: tsResolve}

1. Verify that the {{site.data.keyword.cloud_notm}} integration is active:
   1. In the {{site.data.keyword.sysdigsecure_short}} dashboard, select **Integrations** from the navigation menu, then select **{{site.data.keyword.cloud_notm}}**.
   2. Ensure your account shows as **Connected**.
   3. Check for any error messages in the integration status.

2. Verify that the {{site.data.keyword.appconfig_short}} instance exists and is properly configured:
   1. In the {{site.data.keyword.cloud_notm}} console, select **Resource list** from the navigation menu and locate your {{site.data.keyword.appconfig_short}} instance.
   2. Verify that the {{site.data.keyword.appconfig_short}} instance exists and is in `Active` state.
   3. Verify that the associated trusted profile has the necessary permissions.

3. Check that you have assigned at least the `Manager` role to the {{site.data.keyword.appconfig_short}} service. This is required for CSPM to enable service configuration.

4. Wait for the initial cloud scan to complete. The first scan can take 30-60 minutes after instance provisioning.

5. Verify that your zone contains resources:
   1. In the {{site.data.keyword.sysdigsecure_short}} dashboard, select **Inventory** from the navigation menu, then select **Resources**.
   2. Filter by the zone you created.
   3. Ensure resources are present in the zone.

6. Check for scan failures:
   1. Use the API to query task status: `GET /api/cspm/v1/tasks?filter=type="cloud scan"`
   2. Look for failed scans and review the error details.

7. If the issue persists even after 24 hours, check the [{{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status){: external} for any service disruptions, or contact support for assistance.
