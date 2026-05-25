---

copyright:
  years: 2026
lastupdated: "2026-05-18"

keywords: report download failed, reports manager

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my report failing to generate or download?
{: #ts-report-failures}
{: troubleshoot}
{: support}

You cannot generate compliance reports, or the **Download Report** button fails with an error message.
{: tsSymptoms}

This can occur due to several reasons:
{: tsCauses}

- The report generation service is experiencing issues
- There is no data available for the selected time period or scope
- Browser issues or network connectivity problems
- Insufficient permissions to generate reports

To resolve this issue:
{: tsResolve}

1. Verify that you have the necessary permissions:
   - You need at least `Viewer` role for the {{site.data.keyword.sysdigsecure_short}} service
   - Check your IAM permissions in the {{site.data.keyword.cloud_notm}} console

2. Ensure there is data available for the report:
   - Go to **Compliance** and verify that scan results are visible
   - Check that the time period you selected has completed scans

3. Try generating the report using the API instead of the UI:
   ```bash
   curl -X POST "https://<region>.security-compliance-secure.cloud.ibm.com/api/cspm/v1/reporting/reports" \
     -H "Authorization: Bearer <token>" \
     -H "Content-Type: application/json" \
     -d '{
       "type": "compliance",
       "scope": "zone_id",
       "format": "pdf"
     }'
   ```
   {: pre}

4. Clear your browser cache and cookies, then try again.

5. Check the browser console for errors:
   - Open browser developer tools (F12)
   - Go to the **Console** tab
   - Look for any error messages when clicking **Download Report**
   - Take a screenshot of any errors

6. If scheduled reports are not generating, verify the schedule configuration:
   - Go to **Reporting > Reports Manager**
   - Check that your schedule is active and properly configured
   - Note that there may be a delay between the scheduled time and when the report becomes available.
