---

copyright:
  years: 2026
lastupdated: "2026-06-16"

keywords: inventory missing, data synchronization

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are my resources missing from Inventory?
{: #ts-inventory-missing}
{: troubleshoot}
{: support}

Your agents are running successfully, but hosts or resources do not appear in the **Inventory** tab.
{: tsSymptoms}

This can occur due to several reasons:
{: tsCauses}

- The agent is not properly connected to the {{site.data.keyword.sysdigsecure_short}} instance
- The agent access key is associated with a specific team that you don't have access to
- There is a delay in data synchronization
- The agent is configured for monitoring only and not for security features
- For {{site.data.keyword.cloud_notm}} resources, the {{site.data.keyword.cloud_notm}} integration for your resources is not properly configured.

To resolve this issue:
{: tsResolve}

1. Verify that the agent is running and connected:
   ```bash
   service dragent status
   ```
   {: pre}

2. Check the agent logs for connection errors:
   ```bash
   cat /opt/draios/logs/draios.log | grep -i error
   ```
   {: pre}

3. Verify that you're using the correct agent access key from your {{site.data.keyword.sysdigsecure_short}} instance. If the access key is associated with a specific team, ensure that you have access to that team or use an access key that is not team-specific.

4. For {{site.data.keyword.cloud_notm}} resources, verify the {{site.data.keyword.cloud_notm}} integration status:
   - In the {{site.data.keyword.sysdigsecure_short}} dashboard, go to **Integrations > {{site.data.keyword.cloud_notm}}**
   - Check that your account shows as **Connected** with a recent **Last checked** time
   - If the status shows **Error**, review the error payload for details

5. Wait 5-10 minutes after agent installation for data to appear in the dashboard. Initial synchronization can take time.

6. For Classic Infrastructure resources, ensure that the agent is deployed with the correct collector endpoint for your region. See [Endpoints](/docs/workload-protection?topic=workload-protection-regions#endpoints) for the correct values.
