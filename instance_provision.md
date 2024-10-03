---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning an instance
{: #provision}

You can provision an instance of the {{site.data.keyword.sysdigsecure_full_notm}} service in {{site.data.keyword.cloud_notm}} to add capability in your account to detect and investigate threats, prioritize risks, and help identify compliance anomalies and ongoing threats to your environments.
{: shortdesc}



## Provisioning an instance from the catalog
{: #provision_ui}
{: ui}

To provision an instance from the {{site.data.keyword.cloud_notm}} catalog, complete the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.

2. Click **Catalog**. The list of the services that are available on {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Security** category.

4. Click the **{{site.data.keyword.sysdigsecure_full_notm}}** tile.

5. Select **Create**.

6. Select the location.

7. Select a service plan.

    For more information about the service plans, see [Service plans](/docs/workload-protection?topic=workload-protection-pricing_plans#pricing_plans).

8. Enter a service name.

9. Select a resource group. By default, the **Default** resource group is set.

10. Optionally, you can add tags and access management tags.

11. Click **Create**.



## Provisioning an instance through the CLI
{: #provision_cli}
{: cli}

To provision an instance through the command line, complete the following steps:

1. [Pre-requisite] [Installion of the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli). If the CLI is installed, continue with the next step.

2. Log in to the region in the {{site.data.keyword.cloud_notm}} where you want to provision the instance. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where you want to provision the instance. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Create the instance. Run the [ibmcloud resource service-instance-create](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command:

    ```text
    ibmcloud resource service-instance-create NAME sysdig-secure SERVICE_PLAN_NAME LOCATION
    ```
    {: pre}

    Where

    `NAME` is the name of the instance.

    `service-name` is the name of the {{site.data.keyword.sysdigsecure_full_notm}} service name in the {{site.data.keyword.cloud_notm}}.

    `SERVICE_PLAN_NAME` is the type of plan. See [Service plans](/docs/workload-protection?topic=workload-protection-pricing_plans) to get the plan name.

    `LOCATION` is the region where the instance is created.

5. Create the service key that connects to the instance [ibmcloud resource service-key-create](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_key_create)

    ```text
    ibmcloud resource service-key-create NAME ROLE_NAME --instance-name SERVICE_INSTANCE_NAME
    ```
    {: pre}

    Where

    `NAME` is the name of your new service key

    `ROLE_NAME` is either `Administrator`, `Manager`, `Writer`, or `Reader`

    `SERVICE_INSTANCE_NAME` is the name of the instance you created

    This will gain you access to the instance's access key.
