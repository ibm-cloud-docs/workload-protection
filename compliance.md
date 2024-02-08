---

copyright:
  years:  2023
lastupdated: "2023-09-26"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Analyzing compliance postures from detection to remediation
{: #compliance}

The {{site.data.keyword.sysdigsecure_full}} compliance feature persists environment compliance information in an inventory, which enhances resource visibility and full-context prioritization. This information helps you drive remediation and resolution of compliance violations. {{site.data.keyword.sysdigsecure_short}} supports CSPM and KSPM.
{: shortdesc}

For more information about how an instance of {{site.data.keyword.sysdigsecure_full_notm}} can be integrated with {{site.data.keyword.compliance_short}} to run scans that validate your level of compliance, check out [Connecting Workload Protection](/docs/security-compliance?topic=security-compliance-setup-workload-protection).
{: tip}

Compliance lets you manage your risks by:

* Remediating.
* Accepting the risk.
* Opening Pull requests in your code repository, if integration is enabled.

The resources in your [zones](/docs/workload-protection?topic=workload-protection-zones) are evaluated against compliance policies and any violations are collected as tiles on the **Compliance** page in the {{site.data.keyword.sysdigsecure_full}} UI.  This evaluation is done once daily.

You can use {{site.data.keyword.sysdigsecure_full_notm}} policies or create custom policies.

When evaluating violations you can select the resource to see the associated list of violations.

You can also create reports that you can download from the UI or API.


You can use the {{site.data.keyword.sysdigsecure_full_notm}} **Posture** > **Compliance** view of the {{site.data.keyword.sysdigsecure_short}} UI to review and analyze your environment's compliance posture.

The basic steps you will follow are:

1. Use the [compliance page](/docs/workload-protection?topic=workload-protection-compliance-understanding) to see high-level posture performance indicators (PPIs) for each policy applied to your [zones.](/docs/workload-protection?topic=workload-protection-zones)

2. Select a policy in the view to see its results.

3. Select failing requirements to see the controls and associated failing resources.

4. [Remediate the issues.](/docs/workload-protection?topic=workload-protection-evaluate-remediate) The remediation flow lets you to understand the issue and review suggested patches that {{site.data.keyword.sysdigsecure_full_notm}} creates to resolve the problem. You can also choose to apply the patch manually or by using your Git repository.

    - Manual patches can be applied by copying the provided patch code and applying it to your environment.

    - Remediating using a Git code repository involves selecting the relevant Git source. {{site.data.keyword.sysdigsecure_full_notm}} will create a pull request integrating the patch, as well as checking code formatting. The PR can be reviewed before merging.

    Alternately, you can "accept the risk", either temporarily or permanently, and remove the violation from being flagged by the system.

5. [Create a report.](/docs/workload-protection?topic=workload-protection-compliance-reports) You can optionally generate a compliance report that can be shared with others requiring the information, such as development teams, executives, and auditors.

## Compliance by role
{: #compliance-by-role}

The needs of different members of your organization can be met using the **Compliance** function.

### Compliance and security team members
{: #compliance_sec-team}

Compliance and security team members might need to review the environment's compliance posture in the following areas:

* Checking the current compliance status of the business zones against predefined policies.
* Demonstrating to an auditor the compliance status of their business zone at a specific point in time.
* Creating a report of the compliance status of their business zone to share with auditors and management team.
* Understanding the magnitude of the compliance gap.

### DevOps team members
{: #compliance-devops-team}

DevOps team members might need to review the environment's compliance posture in the following areas:

* Identifying compliance violations for a predefined policy on their business zone.
* Managing violations according to their severity.
* Easily fixing violations.
* Documenting exceptions and acceptable risk according to the risk management policies of their organization.
