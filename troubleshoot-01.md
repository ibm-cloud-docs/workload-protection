---

copyright:
  years:  2023
lastupdated: "2023-05-08"

keywords:

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you receiving a message that credentials cannot be verified when you run a command?
{: #troubleshoot-01}
{: troubleshoot}
{: support}

When you run an {{site.data.keyword.sysdigsecure_full}} command, a message is returned that credentials cannot be verified along with a 401 status.
{: shortdesc}


A message similar to this message is returned when you run a {{site.data.keyword.sysdigsecure_short}} command:

```text
{"message":"cannot verify credentials","referenceId":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}

...

Status: 401, Message: {"message":"cannot verify credentials","referenceId":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```
{: screen}
{: tsSymptoms}

You don't have sufficient permissions to run the command.
{: tsCauses}

Review the documentation on [controlling access through IAM policies](/docs/workload-protection?topic=workload-protection-iam), ensure you have the correct policies set, and retry the command.
{: tsResolve}
