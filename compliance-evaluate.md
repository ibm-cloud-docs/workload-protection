---

copyright:
  years:  2023
lastupdated: "2023-05-14"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Evaluate and remediate
{: #evaluate-remediate}

Once you have reviewed the compliance findings for your environment, you need to evaluate those findings and take the appropriate actions either by resolving any violations or  temporarily accepting them.
{: shortdesc}

## Types of remediation
{: #remediate-type}

The following types of remediation are supported:

Manual remediation
:   The user is presented with text information on how to remediate the violation.

Automatic generation of a patch (with or without user input)
:   Patch code is presented to the user, with input fields to be supplied if values are required. The user then needs to download the patch and add the patch to the application.

Risk is accepted
:   The violation can be marked that the risk has been temporarily accepted.

## Source detection and patching
{: #detect-patch}

{{site.data.keyword.sysdigsecure_full_notm}} attempts to identify the source file matching the violation in your integrated Git repositories. If there are multiple candidates, or if it is not possible to find the matching source file, you can search to find and select the relevant file from the connected Git repositories.

If remediation is possible using a patch, and Git integration is implemented, the **Remediation** page will be available. If multiple files match for the resource, all are displayed as "Suggested Sources". If no files are found, or if you want to remediate a different file, click **Search Source** and  and select the file from the list. Files in connected Git repos will be included in the list.


## Reviewing issues
{: #review-issues}

When you click a zone or policy on the [Compliance page](/docs/workload-protection?topic=workload-protection-compliance-understading) more information on the violations are displayed. By clicking a violation on the [control pane](/docs/workload-protection?topic=workload-protection-compliance-cp) the issues comprising the violation are displayed. By clicking an issue the resources that are passing, failing, or have temporary accepted exceptions are displayed.

By clicking an issue the available remediation options are displayed.

You can see the impact of the remediation, review the resource attributes, and, if needed, enter required values into the patch code.

If a required value can be auto-detected, it will be inserted automatically and the `Value` input field will be read-only.
{: note}

## Verifying patches
{: #verify-patch}

Patch code will be displayed for you to review. Patch code will be displayed if the patch will be applied manually.

You can download the code in the **Continure Remediation** section (preferred) or copy it using cut and paste.

## Applying patches
{: #apply-patch}

### Applying patches manually
{: #manual-patch}

If Git has not been integrated with {{site.data.keyword.sysdigsecure_full_notm}}, you can do a manual remediation.

1. Click **Manually Apply Patch**.

2. Click **Download** to download the patch.

3. Apply the patch to your environment.


## Accepting violation risks
{: #accept-risk}

In some cases a failing control can be safely ignored for a period of time. Accepting the risk will allow the resource to pass and the compliance score for the zome will improve.

In the **Remediation** page:

1. Click **Accept Risk**.

2. Enter the required fields to comply with your organization's audit and best practices.

    Valid reasons are: `Risk Owned`, `Transferred`, `Avoided`, `Mitigated`, `Not Relevant` or `Custom`.

    In the details explain to an auditor the reason for accepting the risk, or the risk management action taken.

    Indicate when you want the risk acceptance to expire and the resource to return to a failed state. Options are 7, 30, 60, or 90 days, a custom time frame, or never.

3. Click **Save**.
