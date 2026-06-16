---

copyright:
  years: 2026
lastupdated: "2026-06-16"

keywords: vulnerabilities not visible, runtime

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are vulnerabilities not appearing?
{: #ts-vulnerabilities-missing}
{: troubleshoot}
{: support}

The **Vulnerabilities** menu is missing from the dashboard, or vulnerabilities are not showing for your resources even though the agent is reporting them.
{: tsSymptoms}

This can occur due to several reasons:
{: tsCauses}

- The agent is not configured to report vulnerability data
- There is a delay in vulnerability data processing
- The resource is listed in inventory but vulnerability scanning has not completed

To resolve this issue:
{: tsResolve}

1. For agent-based vulnerability scanning, verify the agent configuration includes the security features:
   ```yaml
   sysdig:
     accessKey: <your-access-key>
   secure:
     enabled: true
   ```
   {: codeblock}

2. Check the agent logs to confirm vulnerability scanning is active:
   ```bash
   grep -i "vulnerability" /opt/draios/logs/draios.log
   ```
   {: pre}

3. Wait 15-30 minutes after agent deployment for initial vulnerability scans to complete and data to appear in the dashboard.

4. For image vulnerabilities, ensure that the images are being scanned:
   - Go to **Vulnerabilities > Runtime**
   - Check if your container images appear in the list
   - Verify that image scanning is enabled in your pipeline or registry

5. If vulnerabilities appear in agent logs but not in the UI, check the browser console for JavaScript errors and contact {{site.data.keyword.cloud_notm}} support with the error details.
