---

copyright:
  years: 2023, 2026
lastupdated: "2026-10-08"


keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Getting help and support
{: #gettinghelp}

If you have problems or questions when using the {{site.data.keyword.sysdigsecure_full_notm}} service, you have several options to get help with determining the cause of the problem and finding a solution. If you're logged in, you can go directly to the [Support center](https://{DomainName}/unifiedsupport/supportcenter) to review common FAQs, open a support case, or search community content.
{: shortdesc}


## Using the Support Center search field
{: #using-avatar}

You can use the Support Center search field to find answers to your questions from across the {{site.data.keyword.cloud_notm}} documentation and Stack Overflow forum. You can also manage support cases from the Support Center. You can find links to both the Stack Overflow forum for technical questions and the developerWorks (IBM Developer Answers) forum for all other questions under the Forums section of the Support Center.

To access the Support Center, log in to the {{site.data.keyword.cloud_notm}} console, and click **Support** from the menu bar.

If you have a basic, advanced, or premium [support plan](/docs/support?topic=support-open-case&interface=ui), you can find call-in numbers and a chat option to get help.

The Support Center is the preferred method for getting support, but if you can't log in to {{site.data.keyword.cloud_notm}}, you can use the [New support case](https://{DomainName}/unifiedsupport/cases/add) page to submit a case.
{: note}

## Searching forums
{: #asking-a-question}

You can search forums to find answers to your questions. The Stack Overflow forum, for technical questions, and the IBM Developer Answers forum, for general questions, both provide a wide variety of searchable answers to your {{site.data.keyword.cloud_notm}} questions.

If you don't find an existing answer to a question, ask a new one.

You can access Stack Overflow and IBM Developer Answers from the Support Center, or use the following links:

* Go to [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-cloud){: external} to ask technical questions about the {{site.data.keyword.sysdigsecure_full_notm}} service.
* Go to [IBM Developer Answers](https://developer.ibm.com/){: external} to ask general questions about the {{site.data.keyword.sysdigsecure_full_notm}} service and about getting started instructions.

Tag your questions with **ibm-cloud** and **workload-protection**.
{: important}

{{site.data.keyword.cloud_notm}} development and support teams actively monitor Stack Overflow and IBM Developer Answers, and follow the questions that are tagged with **ibm-cloud**. When you create a question in either forum, add the **ibm-cloud** tag to your question to ensure that it's seen by the {{site.data.keyword.cloud_notm}} development and support teams.

## Opening a support case
{: #support_case}

If you don't find answers to your questions, and you experience problems with {{site.data.keyword.cloud_notm}}, you can use support cases to get help with technical, account and access, billing and invoice or sales inquiry issues.

You can [create](/docs/support?topic=support-open-case&interface=ui){: external} and [manage](/docs/support?topic=support-access-cases) a support case by using the [Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}. After you submit a support case, the support team works to investigate and resolve the issue depending on your type of support plan.

## Privacy settings for {{site.data.keyword.cloud_notm}} support access
{: #privacy_settings}

{{site.data.keyword.cloud_notm}} support might need to access your environment to troubleshoot a support case for your instance of {{site.data.keyword.sysdigsecure_full_notm}}. You can use privacy settings to control how {{site.data.keyword.cloud_notm}} support accesses your environment, in addition to the platform and service access controls that are available.

You must have the **Administrator** role to configure support account access and to grant or revoke temporary access for support engineers.
{: note}

To access these settings, open your instance of {{site.data.keyword.sysdigsecure_short}} in the {{site.data.keyword.cloud_notm}} console and click **Open dashboard**. For more information, see [Review Privacy Settings](https://docs.sysdig.com/en/administration/privacy-settings/#review-privacy-settings){: external}.

The following privacy settings are available. When you open a support case, {{site.data.keyword.cloud_notm}} support might ask you to enable specific settings to help diagnose and resolve your issue.

### Global User Settings (Service Analytics)
{: #privacy_global_user_settings}

Global User Settings apply to all users in your account. As an administrator, you can set these settings on behalf of all users. Users can override their own settings if the global settings are enabled.

Usage Data
:   Allows the service to send data about the parts of the application that your users access. Enable this setting if {{site.data.keyword.cloud_notm}} support requests usage telemetry to help investigate a problem. For more information, see [Review Privacy Settings](https://docs.sysdig.com/en/administration/privacy-settings/#review-privacy-settings){: external}.

Crash Reporting
:   Allows the service to send crash reports. Enable this setting if {{site.data.keyword.cloud_notm}} support requests crash report data to diagnose application errors. For more information, see [Review Privacy Settings](https://docs.sysdig.com/en/administration/privacy-settings/#review-privacy-settings){: external}.

### Individual User Settings (Service Analytics)
{: #privacy_individual_user_settings}

If global sharing is enabled by an administrator, individual users can opt out of sharing their own usage and crash data.

Usage Data
:   Allows the service to send data about the parts of the application that an individual user accesses. This setting is available only when the corresponding global setting is enabled.

Crash Reporting
:   Allows the service to send crash reports for an individual user. This setting is available only when the corresponding global setting is enabled.

### {{site.data.keyword.cloud_notm}} Support Account setting
{: #privacy_support_account}

Allows {{site.data.keyword.IBM_notm}} to access your data by using a support account in your environment. When this setting is enabled, an account named **{{site.data.keyword.cloud_notm}} Support** is added to the default team with View Only role. You can manage or remove this account at any time. Enable this setting when {{site.data.keyword.cloud_notm}} support needs persistent read-only access to your environment to investigate a support case. For more information, see [Sysdig Support Account](https://docs.sysdig.com/en/administration/privacy-settings/#sysdig-support-account){: external}.

### Allow User Temporary Access setting
{: #privacy_temp_access}

Allows {{site.data.keyword.cloud_notm}} support engineers to access your data for a fixed duration of up to 30 days. Access ends automatically when the duration expires. Enable this setting when {{site.data.keyword.cloud_notm}} support requests temporary elevated access to reproduce or investigate a time-sensitive issue. For more information, see [Allow User Temporary Access](https://docs.sysdig.com/en/administration/privacy-settings/#allow-user-temporary-access){: external}.
