---

copyright:
  years:  2023
lastupdated: "2023-05-04"

subcollection: workload-protection

keywords: CLI, command line , terminal, shell

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.sysdigsecure_short}} (ibmcloud workload-protection) CLI
{: #workload-protection-cli}

The {{site.data.keyword.cloud}} command-line interface (CLI) provides extra capabilities for service offerings. This information describes how you can use the CLI to access information in {{site.data.keyword.sysdigsecure_full_notm}}.
{: shortdesc}

You can use `wp`, `sysdig-secure`, `security-compliance-secure`, or `scs` as aliases for the `workload-protection` commands. For example, you can run `ibmcloud wp policy create ...`, `ibmcloud sysdig-secure policy create ...`, `ibmcloud security-compliance-secure policy create ...`, or `ibmcloud scs policy create ...` for `ibmcloud workload-protection policy create ...`.
{: note}

## Prerequisites
{: #workload-protection-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.sysdigsecure_full_notm}} CLI by running the following command:

   ```sh
   ibmcloud plugin install workload-protection
   ```
   {: pre}

   Alternately one of the following commands can be used to install the CLI:

   * `ibmcloud plugin install wp`
   * `ibmcloud plugin install sysdig-secure`
   * `ibmcloud plugin install security-compliance-secure`
   * `ibmcloud plugin install scs`

You are notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

## Available CLIs
{: #workload-protection-cli-types}

{{site.data.keyword.sysdigsecure_full_notm}} provides the following CLIs:

[Workload Protection CLI](/docs/workload-protection?topic=workload-protection-workload-protection-cli)
:   Describes how you can use the CLI to access information in IBM Cloud Security and Compliance Center Workload Protection.

[Compliance](/docs/workload-protection?topic=workload-protection-workload-protection-compliance-cli)
:   The compliance CLI lets you determine the available frameworks, platforms, and scope options as well as create and manage benchmark and compliance tasks.

[Policy](/docs/workload-protection?topic=workload-protection-workload-protection-policy-cli)
:   The policies CLI lets you list configured compliance policies.

[Version](/docs/workload-protection?topic=workload-protection-workload-protection-version-cli)
:   The policy CLI lets you determine the version of {{site.data.keyword.sysdigsecure_full_notm}} CLI that is running on your account.
