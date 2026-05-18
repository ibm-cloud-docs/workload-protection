---

copyright:
  years: 2026
lastupdated: "2026-05-18"

keywords: integration errors, IAM, App Configuration

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my {{site.data.keyword.cloud_notm}} integration showing errors?
{: #troubleshoot-integration-errors}
{: troubleshoot}
{: support}

The **Integrations > {{site.data.keyword.cloud_notm}}** page shows your account in **Error** status with error messages.
{: tsSymptoms}

Common error messages include:
{: tsCauses}

- > IBM Token api call failed with error code '500'
- > Exception while getting IBM {{site.data.keyword.appconfig_short}} Account Token
- > Failed to connect to database

To resolve this issue:
{: tsResolve}

1. Verify that the {{site.data.keyword.appconfig_short}} instance exists and is accessible:
   - In the {{site.data.keyword.cloud_notm}} console, go to **Resource list**
   - Locate the {{site.data.keyword.appconfig_short}} instance (typically named `App-Config-SCCWP-CSPM`)
   - Ensure the instance is in `Active` state

2. Check the trusted profile permissions:
   - Go to **Manage > Access (IAM) > Trusted profiles**
   - Locate the trusted profile associated with your {{site.data.keyword.sysdigsecure_short}} instance
   - Verify it has the necessary service-to-service authorizations

3. For database connection errors, these are typically temporary backend issues. Wait 30-60 minutes and check if the error resolves automatically.

4. If the error persists for more than 2 hours, contact {{site.data.keyword.cloud_notm}} support with:
   - Your {{site.data.keyword.sysdigsecure_short}} instance CRN
   - The complete error payload from the integration page
   - The timestamp when the error first appeared.
