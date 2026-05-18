---

copyright:
  years: 2023, 2026
lastupdated: "2026-05-18"

subcollection: workload-protection

keywords: CLI, command line, terminal, shell, compliance, policy, policies

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.sysdigsecure_short}} CLI
{: #workload-protection-cli}

The {{site.data.keyword.cloud}} command-line interface (CLI) provides extra capabilities for service offerings. This information describes how you can use the CLI to manage compliance tasks, policies, and access information in {{site.data.keyword.sysdigsecure_full_notm}}.
{: shortdesc}

You can shorten `workload-protection` to `wp`

You can use `wp`, `sysdig-secure`, `security-compliance-secure`, or `scc` as aliases for the `workload-protection` commands. For example, you can run `ibmcloud wp` instead of `ibmcloud workload-protection` to check which version of the {{site.data.keyword.sysdigsecure_short}} CLI that you're using. 
{: note}

## Prerequisites
{: #workload-protection-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.sysdigsecure_full_notm}} CLI by running the following command:

   ```sh
   ibmcloud plugin install workload-protection
   ```
   {: pre}

You are notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

## Version command
{: #workload-protection-version}

Use this command to determine the version of {{site.data.keyword.sysdigsecure_full_notm}} CLI that is running on your account.

### `ibmcloud workload-protection`
{: #workload-protection-version-cmd}

This command returns the version of {{site.data.keyword.sysdigsecure_full_notm}} CLI that is being run on your account.

```sh
ibmcloud workload-protection (-v | --version)
```
{: pre}

#### Command options
{: #workload-protection-cli-options}

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

## Compliance commands
{: #workload-protection-compliance}

The compliance CLI lets you determine the available frameworks, platforms, and scope options as well as create and manage benchmark and compliance tasks.

### `ibmcloud workload-protection compliance frameworks`
{: #workload-protection-compliance-frameworks}

This command returns a list of available frameworks in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance frameworks (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-frameworks-options}

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance frameworks metadata`
{: #workload-protection-compliance-frameworks-metadata}

This command returns the metadata for the specified framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance frameworks metadata --framework FRAMEWORK (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-frameworks-metadata-options}

`--framework FRAMEWORK`
:   The name of a framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available frameworks can be found using the [`ibmcloud workload-protection compliance frameworks` command](#workload-protection-compliance-frameworks).

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance platforms`
{: #workload-protection-compliance-platforms}

This command returns a list of available platforms in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance platforms (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-platforms-options}

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance scope-options`
{: #workload-protection-compliance-scope-options}

This command returns a list of available scope options in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance scope-options --framework FRAMEWORK --platform PLATFORM [--version VERSION] (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-scope-options-options}

`--framework FRAMEWORK`
:   The name of a framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available frameworks can be found using the [`ibmcloud workload-protection compliance frameworks` command](#workload-protection-compliance-frameworks).

`--platform PLATFORM`
:   The name of a platform in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available platforms can be found using the [`ibmcloud workload-protection compliance platforms` command](#workload-protection-compliance-platforms).

`--version VERSION`
:   Returns the scope labels and operators for only the specified version. If not specified, `Latest` is returned.

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance tasks`
{: #workload-protection-compliance-tasks}

This command lists the tasks configured for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance tasks (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--framework FRAMEWORK] [--filter FILTER] [--version VERSION] [--platform PLATFORM] [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-tasks-options}

`--filter FILTER`
:   Limits results by the string value specified. Only the `name` and `scope` fields are searched for the `filter` value.

`--framework FRAMEWORK`
:   The name of a framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available frameworks can be found using the [`ibmcloud workload-protection compliance frameworks` command](#workload-protection-compliance-frameworks).

`--platform PLATFORM`
:   The name of a platform in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available platforms can be found using the [`ibmcloud workload-protection compliance platforms` command](#workload-protection-compliance-platforms).

`--version VERSION`
:   Returns the tasks for the specified version. If not specified, `Latest` is returned.

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance task create`
{: #workload-protection-compliance-task-create}

This command creates a new compliance task in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task create --name NAME --schedule SCHEDULE --framework FRAMEWORK --platform PLATFORM --version VERSION [--scope SCOPE] [--schema SCHEMA] [--enabled ENABLED] [--excludeControlList CONTROL_IDS]
```
{: pre}

#### Command options
{: #workload-protection-compliance-task-create-options}

`--enabled ENABLED`
:   Indicates if the task is enabled, and can be run, or is disabled. Valid values are `true` and `false`. Default is `false` indicating that the task is not enabled.

`--excludeControlList CONTROL_IDS`
:   List of control IDs to be excluded from compliance task.

`--framework FRAMEWORK`
:   The name of a framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available frameworks can be found using the [`ibmcloud workload-protection compliance frameworks` command](#workload-protection-compliance-frameworks).

`--name NAME`
:   The name to be given to the task.

`--platform PLATFORM`
:   The name of a platform in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available platforms can be found using the [`ibmcloud workload-protection compliance platforms` command](#workload-protection-compliance-platforms).

`--schedule SCHEDULE`
:   The schedule when the task will be run. Specify as a cron-like expression representing a frequency. For example, `0 10 * * 1`.

`--schema SCHEMA`
:   The benchmark or compliance schema to be applied to the task. Valid values are:

    * `kube_bench_cis-1.5`
    * `kube_bench_cis-1.6`
    * `kube_bench_gke-1.0`
    * `kube_bench_eks-1.0`
    * `kube_bench_rh-0.7`
    * `linux_bench_cis-1.1`
    * `docker_bench_security_1.0`
    * `aws_foundations_bench-1.3`
    * `NIST-800-53-Rev4-WORKLOAD`
    * `NIST-800-53-Rev4-AWS`
    * `NIST-800-53-Rev5-WORKLOAD`
    * `NIST-800-53-Rev5-AWS`
    * `NIST-800-190-WORKLOAD`

`--scope SCOPE`
:   The task scope.

`--version VERSION`
:   You can optionally specify the version of the framework. If not specified, defaults to `Latest`.

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance task delete`
{: #workload-protection-compliance-task-delete}

This command deletes a task defined in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task delete --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-task-delete-options}

`--id ID`
:   The task ID of the compliance task. You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command](#workload-protection-compliance-tasks).

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance task update`
{: #workload-protection-compliance-task-update}

This command enables or disables a task defined in your {{site.data.keyword.sysdigsecure_full_notm}} instance. A disabled task cannot be run.

```sh
ibmcloud workload-protection compliance task update --id ID (--disable | --enable)
```
{: pre}

#### Command options
{: #workload-protection-compliance-task-update-options}

`--id ID`
:   The task ID of the compliance task. You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command](#workload-protection-compliance-tasks).

`--disable`
:   The task ID is disabled and will not run.

`--enable`
:   The task ID is enabled and will run.

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance task get`
{: #workload-protection-compliance-task-get}

This returns the task defined by the specified ID in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task get --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-task-get-options}

`--id ID`
:   The task ID of the compliance task. You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command](#workload-protection-compliance-tasks).

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance task report`
{: #workload-protection-compliance-task-report}

This command returns the latest report for the task defined in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task report --id ID [--report-id REPORT_ID] (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-task-report-options}

`--id ID`
:   The task ID of the compliance task. You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command](#workload-protection-compliance-tasks).

`--report-id REPORT_ID`
:   The report ID. If not specified, the `latest` will be returned.

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection compliance task run`
{: #workload-protection-compliance-task-run}

This command runs a task defined in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task run --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-compliance-task-run-options}

`--id ID`
:   The task ID of the compliance task. You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command](#workload-protection-compliance-tasks).

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

## Policy commands
{: #workload-protection-policy}

The policy CLI lets you create and manage compliance policies.

### `ibmcloud workload-protection policies`
{: #workload-protection-policies}

This command lists all the policies defined for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policies (--instance-id ID | --instance-name INSTANCE_NAME) [--default] [--severity SEVERITY] [--filter FILTER] [--limit LIMIT] [--offset OFFSET]
```
{: pre}

#### Command options
{: #workload-protection-policies-options}

`--default`
:   Lists the default policies for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

`--filter FILTER`
:   A string to look for in the policy names or descriptions.

`--limit LIMIT`
:   The number of items to be returned. This is an integer value from 1 to 100.

`--offset OFFSET`
:   The number of returned items to be skipped before starting to return policies. For example `--offset 20` will skip the first 20 policies before returning policies up to the number of items specified by `--limit`.

`--severity SEVERITY`
:   Returns the policies with the specified severity value. For example, `--severity 3`.

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection policy create`
{: #workload-protection-policy-create}

This command creates a security policy for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policy create (--payload FILE | JSON) (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--default] [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-policy-create-options}

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

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection policy delete`
{: #workload-protection-policy-delete}

This command deletes a security policy in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policy delete --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-policy-delete-options}

`--id ID`
:   The policy ID of the policy. You can find a list of policies by running the [`ibmcloud workload-protection policies` command](#workload-protection-policies).

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection policy get`
{: #workload-protection-policy-get}

This command returns a security policy in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policy get --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-policy-get-options}

`--id ID`
:   The policy ID of the policy. You can find a list of policies by running the [`ibmcloud workload-protection policies` command](#workload-protection-policies).

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.

### `ibmcloud workload-protection policy update`
{: #workload-protection-policy-update}

This command updates an existing security policy for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection policy update --id ID (--payload FILE | JSON) (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

#### Command options
{: #workload-protection-policy-update-options}

`--id ID`
:   The policy ID of the policy. You can find a list of policies by running the [`ibmcloud workload-protection policies` command](#workload-protection-policies).

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

`--instance-id ID` (required), exclusive with `--instance-name`
:   The ID of the {{site.data.keyword.sysdigsecure_full_notm}} instance. The ID can be obtained by running the [`ibmcloud resource service-instance` command](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance). One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--instance-name INSTANCE_NAME` (required), exclusive with `--instance-id`
:   The name of the {{site.data.keyword.sysdigsecure_full_notm}} instance. This is the [name](/docs/workload-protection?topic=workload-protection-provision) you specified when creating the instance. One of `--instance-id` or `--instance-name` must be specified. The `--instance-id` and `--instance-name` options cannot be specified together on the same command invocation.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Available output formats are `JSON`, `YAML`, or `TABLE`. If not specified, output will be returned in a tabular format.

`--quiet` | `-q`
:   Suppress verbose messages.

`help` | `--help` | `-h`
:   List options available for the command.
