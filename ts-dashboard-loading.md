---

copyright:
  years: 2026
lastupdated: "2026-06-16"

keywords: dashboard not loading, resource list

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my dashboard not loading or showing errors?
{: #ts-dashboard-loading}
{: troubleshoot}
{: support}

When you try to access the {{site.data.keyword.sysdigsecure_short}} dashboard, it does not load, shows a blank page, or displays error messages like:
{: tsSymptoms}

- > An error has occurred
- > OPEN_ID_AUTHORIZATION_ERROR


This can occur due to several reasons:
{: tsCauses}

- Authentication or authorization issues
- Browser compatibility or cache issues
- Service disruption or maintenance
- Network connectivity problems
- The instance is not fully provisioned

To resolve this issue:
{: tsResolve}

1. Verify that you have the necessary permissions:
   - You need at least `Viewer` role for the {{site.data.keyword.sysdigsecure_short}} service
   - Check your IAM permissions in the {{site.data.keyword.cloud_notm}} console under **Manage > Access (IAM)**

2. Clear your browser cache and cookies.

3. Try accessing the dashboard in a `private or incognito browser window` to rule out browser extension issues.

4. Verify that the instance is fully provisioned:
   - In the {{site.data.keyword.cloud_notm}} console, go to **Resource list**
   - Check that your {{site.data.keyword.sysdigsecure_short}} instance shows as `Active`
   - Wait at least 10-15 minutes after instance creation before accessing the dashboard

5. Check the {{site.data.keyword.cloud_notm}} status page for any service disruptions:
   - Go to [{{site.data.keyword.cloud_notm}} Status](https://cloud.ibm.com/status){: external}
   - Look for any incidents affecting {{site.data.keyword.sysdigsecure_short}}

6. Try accessing the dashboard from a different network to rule out network-related issues.
