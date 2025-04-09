---

copyright:
  years:  2023
lastupdated: "2023-05-04"

subcollection: workload-protection

keywords: CLI, command line , terminal, shell, compliance

---

{{site.data.keyword.attribute-definition-list}}


# Compliance (ibmcloud workload-protection compliance) CLI
{: #workload-protection-compliance-cli}

The {{site.data.keyword.sysdigsecure_full}} compliance CLI lets you determine the available frameworks, platforms, and scope options as well as create and manage benchmark and compliance tasks.
{: shortdesc}

You can use `wp`, `sysdig-secure`, `security-compliance-secure`, or `scs` as aliases for the `workload-protection` commands. For example, you can run `ibmcloud wp policy create ...`, `ibmcloud sysdig-secure policy create ...`, `ibmcloud security-compliance-secure policy create ...`, or `ibmcloud scs policy create ...` for `ibmcloud workload-protection policy create ...`.
{: note}

## Concepts
{: #workload-protection-concepts}

To use this CLI you will need to understand the following {{site.data.keyword.sysdigsecure_full_notm}} concepts. For more information on {{site.data.keyword.sysdigsecure_full_notm}}, see the [{{site.data.keyword.sysdigsecure_full_notm}} documentation.](/docs/workload-protection?topic=workload-protection-getting-started)

* Compliance frameworks provide guidelines and structures to maintain security and help meet regulatory requirements.

* Compliance platforms include the available platforms to be monitored including platforms such as Kubernetes, Docker, and so on.

* Scope options are the available scope labels and operators that can be used when creating a benchmark or compliance task.

* Tasks allow you to create benchmarks or compliance tasks.

## Command options
{: #ss_compliance_options}

The following are the available options for all `ibmcloud workload-protection compliance` commands.

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

## ibmcloud workload-protection compliance frameworks
{: #ss_compliance_frameworks}

This command returns a list of available frameworks in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance frameworks (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Frameworks command options
{: #ss_compliance_frameworks_options}

See the [command options](#ss_compliance_options) for a description of each option.

## ibmcloud workload-protection compliance frameworks metadata
{: #ss_compliance_frameworksmetadata}

This command returns the metadata for the specified framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance frameworks metadata --framework FRAMEWORK (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Frameworks metadata command options
{: #ss_compliance_frameworksmetadata_options}

`--framework FRAMEWORK`
:   The name of a framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available frameworks can be found using the [`ibmcloud workload-protection compliance frameworks` command.](#ss_compliance_frameworks)

See the [command options](#ss_compliance_options) for a description of additional options.

## ibmcloud workload-protection compliance platforms
{: #ss_compliance_platforms}

This command returns a list of available platforms in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance platforms (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Platforms command options
{: #ss_compliance_platforms_options}

See the [command options](#ss_compliance_options) for a description of each option.

## ibmcloud workload-protection compliance scope-options
{: #ss_compliance_scopeoptions}

This command returns a list of available scope options in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance scope-options --framework FRAMEWORK --platform PLATFORM [--version VERSION] (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Compliance scope-options command options
{: #ss_compliance_scopeoptions_options}

`--framework FRAMEWORK`
:   The name of a framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available frameworks can be found using the [`ibmcloud workload-protection compliance frameworks` command.](#ss_compliance_frameworks)

`--platform PLATFORM`
:   The name of a platform in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available platforms can be found using the [`ibmcloud workload-protection compliance platforms` command.](#ss_compliance_platforms)

`--version VERSION`
:   Returns the scope labels and operators for only the specified version. If not specified, `Latest` is returned.

See the [command options](#ss_compliance_options) for a description of additional options.

## ibmcloud workload-protection compliance tasks
{: #ss_compliance_tasklist}

This command lists the tasks configured for your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance tasks (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--framework FRAMEWORK] [--filter FILTER] [--version VERSION] [--platform PLATFORM] [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Compliance tasks command options
{: #ss_compliance_tasks_options}

`--filter FILTER`
:   Limits results by the string value specified. Only the `name` and `scope` fields are searched for the `filter` value.

`--framework FRAMEWORK`
:   The name of a framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available frameworks can be found using the [`ibmcloud workload-protection compliance frameworks` command.](#ss_compliance_frameworks)

`--platform PLATFORM`
:   The name of a platform in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available platforms can be found using the [`ibmcloud workload-protection compliance platforms` command.](#ss_compliance_platforms)

`--version VERSION`
:   Returns the tasks for the specified version. If not specified, `Latest` is returned.

See the [command options](#ss_compliance_options) for a description of additional options.

## ibmcloud workload-protection compliance task create
{: #ss_compliance_taskcreate}

This command creates a new compliance task in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task create --name NAME --schedule SCHEDULE --framework FRAMEWORK --platform PLATFORM --version VERSION [--scope SCOPE] [--schema SCHEMA] [--enabled ENABLED] [--excludeControlList CONTROL_IDS]
```
{: pre}

### Compliance task create command options
{: #ss_compliance_taskcreate_options}

`--enabled ENABLED`
:   Indicates if the task is enabled, and can be run, or is disabled. Valid values are `true` and `false`. Default is `false` indicating that the task is not enabled.

`--excludeControlList CONTROL_IDS`
:   List of control IDs to be excluded from compliance task.

`--framework FRAMEWORK`
:   The name of a framework in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available frameworks can be found using the [`ibmcloud workload-protection compliance frameworks` command.](#ss_compliance_frameworks)

`--name NAME`
:   The name to be given to the task.

`--platform PLATFORM`
:   The name of a platform in your {{site.data.keyword.sysdigsecure_full_notm}} instance. Available platforms can be found using the [`ibmcloud workload-protection compliance platforms` command.](#ss_compliance_platforms)

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


See the [command options](#ss_compliance_options) for a description of additional options.

## ibmcloud workload-protection compliance task delete
{: #ss_compliance_taskdelete}

This command deletes a task defined in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task delete --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Compliance task delete command options
{: #ss_compliance_taskdelete_options}

`--id ID`
:   The task ID of the compliance task.  You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command.](#ss_compliance_tasklist)

See the [command options](#ss_compliance_options) for a description of additional options.

## ibmcloud workload-protection compliance task update
{: #ss_compliance_taskupdate}

This command enables or disables a task defined in your {{site.data.keyword.sysdigsecure_full_notm}} instance. A disabled task cannot be run.

```sh
ibmcloud workload-protection compliance task update --id ID (--disable | --enable)
```
{: pre}

### Compliance task update command options
{: #ss_compliance_taskupdate_options}

`--id ID`
:   The task ID of the compliance task.  You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command.](#ss_compliance_tasklist)

`--disable`
:   The task ID is disabled and will not run.

`--enable`
:   The task ID is enabled and will run.

See the [command options](#ss_compliance_options) for a description of additional options.

## ibmcloud workload-protection compliance task get
{: #ss_compliance_taskget}

This returns the task defined by the specified ID in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task get --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Compliance task get command options
{: #ss_compliance_tasklist_options}


`--id ID`
:   The task ID of the compliance task.  You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command.](#ss_compliance_tasklist)

See the [command options](#ss_compliance_options) for a description of additional options.

## ibmcloud workload-protection compliance task report
{: #ss_compliance_taskreport}

This command returns the latest report for the task defined in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task report --id ID --report-id REPORT_ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Compliance task report command options
{: #ss_compliance_taskreport_options}

`--id ID`
:   The task ID of the compliance task.  You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command.](#ss_compliance_tasklist)

`--report-id REPORT_ID`
:   The report ID. If not specified, the `latest` will be returned.

See the [command options](#ss_compliance_options) for a description of additional options.

## ibmcloud workload-protection compliance task run
{: #ss_compliance_taskrun}

This command runs a task defined in your {{site.data.keyword.sysdigsecure_full_notm}} instance.

```sh
ibmcloud workload-protection compliance task run --id ID (--instance-id INSTANCE_ID | --instance-name INSTANCE_NAME) [--region REGION] [--output FORMAT] [--quiet]
```
{: pre}

### Compliance task run command options
{: #ss_compliance_taskrun_options}

`--id ID`
:   The task ID of the compliance task.  You can find a list of configured tasks by running the [`ibmcloud workload-protection compliance tasks` command.](#ss_compliance_tasklist)

See the [command options](#ss_compliance_options) for a description of additional options.
