---

copyright:
  years: 2026
lastupdated: "2026-05-18"

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

- The cloud scan has not completed yet
- The {{site.data.keyword.cloud_notm}} integration is not properly configured
- The {{site.data.keyword.appconfig_short}} instance or trusted profile was not created correctly
- There are no resources in the zone that match the policy requirements
- The scan failed due to backend errors

To resolve this issue:
{: tsResolve}

1. Verify that the {{site.data.keyword.cloud_notm}} integration is active:
   - Go to **Integrations > {{site.data.keyword.cloud_notm}}**
   - Ensure your account shows as **Connected**
   - Check for any error messages in the integration status

2. Verify that the {{site.data.keyword.appconfig_short}} instance exists and is properly configured:
   - In the {{site.data.keyword.cloud_notm}} console, go to **Resource list**
   - Look for an {{site.data.keyword.appconfig_short}} instance named `App-Config-SCCWP-CSPM`
   - Verify that the associated trusted profile has the necessary permissions

3. Check that you have assigned at least the `Manager` role to the {{site.data.keyword.appconfig_short}} service. This is required for CSPM to enable service configuration.

4. Wait for the initial cloud scan to complete. The first scan can take 30-60 minutes after instance provisioning.

5. Verify that your zone contains resources:
   - Go to **Inventory > Resources**
   - Filter by the zone you created
   - Ensure resources are present in the zone

6. Check for scan failures:
   - Use the API to query task status: `GET /api/cspm/v1/tasks?filter=type="cloud scan"`
   - Look for failed scans and review the error details

7. If the issue persists after 24 hours, check the {{site.data.keyword.cloud_notm}} status page for any service disruptions.
