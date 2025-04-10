---

copyright:
  years:  2023
lastupdated: "2023-05-04"

subcollection: workload-protection

keywords: CLI, command line , terminal, shell, compliance, policy, policies

---

{{site.data.keyword.attribute-definition-list}}


# Policy (ibmcloud workload-protection policy & policies) CLIs
{: #workload-protection-policy-cli}

The {{site.data.keyword.sysdigsecure_full}} policy CLI lets you create and manage compliance policies.
{: shortdesc}

You can use `wp`, `sysdig-secure`, `security-compliance-secure`, or `scs` as aliases for the `workload-protection` commands. For example, you can run `ibmcloud wp policy create ...`, `ibmcloud sysdig-secure policy create ...`, `ibmcloud security-compliance-secure policy create ...`, or `ibmcloud scs policy create ...` for `ibmcloud workload-protection policy create ...`.
{: note}

## Concepts
{: #workload-protection-policy-concepts}

To use this CLI you will need to understand the following {{site.data.keyword.sysdigsecure_full_notm}} concepts. For more information on {{site.data.keyword.sysdigsecure_full_notm}}, see the [{{site.data.keyword.sysdigsecure_full_notm}} documentation.](/docs/workload-protection?topic=workload-protection-getting-started)

* You can configure a policy on a resource and define what to do when 1 or more rules that are included in the policy are non-compliant.

* {{site.data.keyword.sysdigsecure_full_notm}} includes a number of pre-defined policies that you can use.

* The `policy` CLI lets you manage and create policies. The `policies` CLI list information about policies configured in the service instance.

## Command options
{: #ss_policy_options}

The following are the available options for all `ibmcloud workload-protection policy` and `ibmcloud workload-protection policies` commands.

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command.](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance) One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance.  This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`.  If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud workload-protection policies
{: #ss_policy_policylist}

This command list all the policies defined for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policies (--instance-id ID | --instance-name INSTANCE_NAME) [--default] [--severity SEVERITY] [--filter FILTER] [--limit LIMIT] [--offset OFFSET]
```
{: pre}

### Policies command options
{: #ss_policy_policies_options}

`--default`
:   Lists the default policies for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

`--filter FILTER`
:   A string to look for in the policy names or descriptions.

`--limit LIMIT`
:   The number of items to be returned. This is an integer value from 1 to 100.

`--offset OFFSET`
:   The number of returned items to be skipped before starting to return policies. For example `--offset 20` will skip the first 20 policies before returning policies up to the number of items specified by `--limit`.

`--severity SEVERITY`
:   Returns the policies with the specified severity value.  For example, `--severity 3`.

## ibmcloud workload-protection policy create
{: #ss_policy_create}

This command creates a security policy for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policy create (--instance-id ID | --instance-name NAME) (--payload FILE | JSON) (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--default] [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Policy create command options
{: #ss_policy_create_options}

`--default`
:   Specifies the policy is a default policy for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

`--payload FILE | JSON`
:   Either a file containing the policy definition in JSON format or the policy definition in JSON format.

A policy definition would be similar to the following:

```json
{
  "name": "Check filesystem activity",
  "description": "Monitor all filesystem operations and look for suspicious or notable behavior",
  "enabled": true,
  "scope": "container.image.repo = \"sysdig/agent\"",
  "ruleNames": [],
  "notificationChannelIds": [],
  "severity": 0,
  "actions": [
    {
      "afterEventNs": 1000000000,
      "beforeEventNs": 1000000000,
      "isLimitedToContainer": false,
      "type": "POLICY_ACTION_CAPTURE",
      "filter": "proc.name=cat or proc.name=vi",
      "name": "string",
      "bucketName": "",
      "storageType": "S3"
    }
  ],
  "type": "falco"
}
```
{: codeblock}

See the [command options](#ss_policy_options) for a description of additional options.

## ibmcloud workload-protection policy delete
{: #ss_policy_delete}

This command deletes a security policy in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policy delete --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Policy delete command options
{: #ss_policy_delete_options}

`--id ID`
:   The policy ID of the policy.  You can find a list of policies by running the [`ibmcloud workload-protection policies` command.](#ss_policy_policylist)

See the [command options](#ss_policy_options) for a description of additional options.

## ibmcloud workload-protection policy get
{: #ss_policy_get}

This command returns a security policy in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policy get --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Policy get command options
{: #ss_policy_get_options}

`--id ID`
:   The policy ID of the policy.  You can find a list of policies by running the [`ibmcloud workload-protection policies` command.](#ss_policy_policylist)

See the [command options](#ss_policy_options) for a description of additional options.

## ibmcloud workload-protection policy update
{: #ss_policy_update}

This command updates an existing security policy for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policy update --ID ID (--payload FILE | JSON) (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Policy update command options
{: #ss_policy_update_options}

`--id ID`
:   The policy ID of the policy.  You can find a list of policies by running the [`ibmcloud workload-protection policies` command.](#ss_policy_policylist)

`--payload FILE | JSON`
:   Either a file containing the policy definition in JSON format or the policy definition in JSON format.

A policy definition would be similar to the following:

```json
{
  "name": "Check filesystem activity",
  "description": "Monitor all filesystem operations and look for suspicious or notable behavior",
  "enabled": true,
  "scope": "container.image.repo = \"sysdig/agent\"",
  "ruleNames": [],
  "notificationChannelIds": [],
  "severity": 0,
  "actions": [
    {
      "afterEventNs": 1000000000,
      "beforeEventNs": 1000000000,
      "isLimitedToContainer": false,
      "type": "POLICY_ACTION_CAPTURE",
      "filter": "proc.name=cat or proc.name=vi",
      "name": "string",
      "bucketName": "",
      "storageType": "S3"
    }
  ],
  "type": "falco"
}
```
{: codeblock}

See the [command options](#ss_policy_options) for a description of additional options.
