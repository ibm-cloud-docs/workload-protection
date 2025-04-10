---

copyright:
  years:  2023
lastupdated: "2023-05-04"

subcollection: workload-protection

keywords: CLI, command line , terminal, shell, compliance, version

---

{{site.data.keyword.attribute-definition-list}}


# Version (ibmcloud workload-protection) CLI
{: #workload-protection-version-cli}

The {{site.data.keyword.sysdigsecure_full}} version CLI option lets you determine the version of {{site.data.keyword.sysdigsecure_full_notm}} CLI that is running on your account.
{: shortdesc}

You can use `wp`, `sysdig-secure`, `security-compliance-secure`, or `scs` as aliases for the `workload-protection` commands. For example, you can run `ibmcloud wp policy create ...`, `ibmcloud sysdig-secure policy create ...`, `ibmcloud security-compliance-secure policy create ...`, or `ibmcloud scs policy create ...` for `ibmcloud workload-protection policy create ...`.
{: note}

## ibmcloud workload-protection
{: #ss_version}

This command returns the version of {{site.data.keyword.sysdigsecure_full_notm}} CLI that is being run on your account.

```sh
ibmcloud workload-protection (-v | --version)
```
{: pre}
