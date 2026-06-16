---

copyright:
  years:  2024, 2026
lastupdated: "2026-06-16"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Enabling cloud compliance with CSPM
{: #cspm-implement}

Enable cloud security posture management (CSPM) in {{site.data.keyword.sysdigsecure_short}} to scan your {{site.data.keyword.cloud_notm}} resources for compliance with security and regulatory frameworks. With CSPM enabled, {{site.data.keyword.sysdigsecure_short}} continuously evaluates your cloud resources against predefined policies, helping you identify and resolve issues before they become security risks.
{: shortdesc}

This topic focuses on enabling CSPM for {{site.data.keyword.cloud_notm}}. Need to enable CSPM for another cloud provider, like AWS, Azure, GCP, or OCI? See [Connect cloud accounts](https://docs.sysdig.com/en/sysdig-secure/connect-cloud-accounts/){: external} for more information.
{: tip}

To learn more about CSPM and how it works, go to [About {{site.data.keyword.sysdigsecure_short}}](/docs/workload-protection?topic=workload-protection-about). To see an example workflow, go to [Analyzing compliance postures from detection to remediation](/docs/workload-protection?topic=workload-protection-compliance). 

CSPM for {{site.data.keyword.sysdigsecure_short}} depends on {{site.data.keyword.appconfig_short}}, which collects configuration details from your {{site.data.keyword.cloud_notm}} resources. The [configuration aggregator feature](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator) in {{site.data.keyword.appconfig_short}} is included at no charge as part of the Lite plan. The integration uses [IAM trusted profiles](/docs/account?topic=account-create-trusted-profile&interface=ui) to manage permissions securely.

You can enable CSPM for individual {{site.data.keyword.cloud_notm}} accounts or for your entire enterprise. For enterprise-level compliance scanning, see [Enabling cloud compliance for enterprises](/docs/workload-protection?topic=workload-protection-cspm-tutorial-enterprise).

CSPM is enabled by default when you create an instance of {{site.data.keyword.sysdigsecure_short}}. However, if you decide to disable it, you can enable it at any time by completing the following steps. For more information on creating an instance of {{site.data.keyword.sysdigsecure_short}} with CSPM enabled, see [Getting started](/docs/workload-protection?topic=workload-protection-getting-started&interface=ui#setup).
{: tip}

## Before you begin
{: #cspm-implement-prereqs-ui}

Before you get started, make sure that you have the following:

- An existing {{site.data.keyword.appconfig_short}} instance. For more information, see [Creating an instance](/docs/app-configuration?topic=app-configuration-ac-create-an-instance).
- `Manager` role or greater on the [{{site.data.keyword.appconfig_short}} service](/docs/app-configuration?topic=app-configuration-ac-service-access-management).
- An existing {{site.data.keyword.sysdigsecure_short}} instance with CSPM disabled. For more information, see [Set up {{site.data.keyword.sysdigsecure_short}}](/docs/workload-protection?topic=workload-protection-cspm-tutorial-enterprise#setup-wp).
- [Permissions to create and manage trusted profiles](/docs/account?topic=account-create-trusted-profile&interface=ui#tp-roles-reqs).
- `Editor` role or greater on the {{site.data.keyword.sysdigsecure_short}} service.
- The CRNs for your {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.appconfig_short}} instances. If you don't already have them, you can find the CRNs by completing the following steps: 
    1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list** and search for the service, either {{site.data.keyword.sysdigsecure_short}} or {{site.data.keyword.appconfig_short}}. 
    2. After you open your instance of {{site.data.keyword.appconfig_short}}, click **Details** and copy the CRN. 
    3. After you open your instance of {{site.data.keyword.sysdigsecure_short}}, copy the CRN from the Details panel. 

If context-based restrictions are enabled for resources in your account, you must create a rule to allow {{site.data.keyword.appconfig_short}} to collect configuration data. When creating the rule, [select {{site.data.keyword.appconfig_short}} as the reference service](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator#ac-configuration-aggregator-with-workload-protection).
{: important}

<!-- ## Before you begin
{: #cspm-implement-prereqs-cli}
{: cli}

Before you get started, make sure that you have the following:

- An existing {{site.data.keyword.appconfig_short}} instance. For more information, see [Creating an instance](/docs/app-configuration?topic=app-configuration-ac-create-an-instance).
- `Manager` role or greater on the [{{site.data.keyword.appconfig_short}} service](/docs/app-configuration?topic=app-configuration-ac-service-access-management).
- An existing {{site.data.keyword.sysdigsecure_short}} instance with CSPM disabled. For more information, see [Set up {{site.data.keyword.sysdigsecure_short}}](/docs/workload-protection?topic=workload-protection-cspm-tutorial-enterprise#setup-wp).
- [Permissions to create and manage trusted profiles](/docs/account?topic=account-create-trusted-profile&interface=ui#tp-roles-reqs).
- `blank` role or greater on the {{site.data.keyword.sysdigsecure_short}} service.
- Install the [stand-alone {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).
- Install the [{{site.data.keyword.sysdigsecure_short}} CLI plug-in](/docs/cli?topic=cli-plug-ins#cli-search-plugin).
- The CRNs and names of your {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.appconfig_short}} instances. You also need the instance ID for your {{site.data.keyword.appconfig_short}} instance. You can find this information by running the [`ibmcloud resource service-instances`](/docs/cli/build/cli-review-output?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instances) command.
    - To retrieve the information for your {{site.data.keyword.sysdigsecure_short}} instance, run `ibmcloud resource service-instances --service-name sysdig-secure --long`.
    - To retrieve the information for your {{site.data.keyword.appconfig_short}} instance, run `ibmcloud resource service-instances --service-name apprapp --long`.
    
    The instance ID is identified as the `GUID` in the CLI output. 
    {: important}

- Get your {{site.data.keyword.cloud_notm}} account ID. You can find the account ID by running the [`ibmcloud account show`](/docs/cli/build/cli-review-output?topic=cli-ibmcloud_commands_account#ibmcloud_account_show) command. 

If context-based restrictions are enabled for resources in your account, you must create a rule to allow {{site.data.keyword.appconfig_short}} to collect configuration data. When creating the rule, [select {{siede.data.keyword.appconfig_short}} as the reference service](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator#ac-configuration-aggregator-with-workload-protection).
{: important} -->

## Creating a trusted profile
{: #tp-create}

[Create a trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui) that allows your instance of {{site.data.keyword.sysdigsecure_short}} access to the {{site.data.keyword.appconfig_short}} service. Completing the following steps: 

1. Go to **Manage > Access (IAM) > Trusted profiles** and click **Create**.
2. After providing a name for the trusted profile, establish trust by selecting **{{site.data.keyword.cloud_notm}} services** as the trusted entity type, and enter the CRN for your {{site.data.keyword.sysdigsecure_short}} instance.
4. Add the following access policies to the trusted profile:
    * Viewer and Usage Report Viewer roles on the Enterprise service.
    * Configuration Aggregator Reader and Manager roles on the {{site.data.keyword.appconfig_short}} service.
5. After you create the trusted profile, copy the profile ID and save it for the next step.

## Connecting your {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.sysdigsecure_short}}
{: #cspm-implement-ui}

To start scanning your {{site.data.keyword.cloud_notm}} account for compliance, add it to your existing {{site.data.keyword.sysdigsecure_short}} instance. By doing so, you enable CSPM for your {{site.data.keyword.cloud_notm}} account.

1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Security > Compliance** then click the name of your instance of {{site.data.keyword.sysdigsecure_short}}.
2. Click **Sources**, then select the **{{site.data.keyword.cloud_notm}} Account** tab.
3. Click **Add** and enter the trusted profile ID that you just created along with the CRN for your instance of {{site.data.keyword.appconfig_short}}.
4. Click **Add** to save your changes.

## Enabling configuration aggregator in {{site.data.keyword.appconfig_short}}
{: #cspm-implement-ui-ca}

Your instance of {{site.data.keyword.sysdigsecure_short}} is now connected to your instance of {{site.data.keyword.appconfig_short}}. However, configuration aggregator within {{site.data.keyword.appconfig_short}} must be enabled to gather information from your {{site.data.keyword.cloud_notm}} account and resources. Complete the following steps: 

1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list** and search for `App Configuration`. 
2. Click the name of the {{site.data.keyword.appconfig_short}} instance to open it. 
3. Click **Configuration aggregator > Define an aggregation**. 
4. Select **All regions** to gather data from all regions, and click **Save**.
5. Enable **Recording** to begin collecting configuration data. 

Compliance scan results appear within 5-10 minutes after provisioning, depending on the number of resources in your account.

## Disabling CSPM
{: #cspm-implement-ui-disable}

To stop scanning your {{site.data.keyword.cloud_notm}} account for compliance, disable CSPM.

1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Security > Compliance** then click the name of your instance of {{site.data.keyword.sysdigsecure_short}}.
2. Click **Sources**, then select the **{{site.data.keyword.cloud_notm}} Account** tab.
3. Click the actions menu for the account you want to remove, then click **Remove**.

Compliance scanning stops for the selected account.



<!-- ### Connect your account to {{site.data.keyword.sysdigsecure_short}} by using the CLI
{: #cspm-implement-cli-step5}
{: cli}

Connect your {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.sysdigsecure_short}} to start scanning for compliance.

```sh
ibmcloud resource service-instance-update "<workload_protection_instance_name>" -p '{"enable_cspm": true, "target_accounts": [{"account_id": "<ibm_cloud_account_id>", "config_crn": "<app_configuration_instance_CRN>", "trusted_profile_id": "<tp_id_for_wp>"}]}' -g Default
```
{: pre} -->




<!-- 
## Disabling CSPM by using the CLI
{: #cspm-implement-disable}
{: cli}

To stop scanning your account for compliance, run the following command. Replace the placeholder values with your {{site.data.keyword.sysdigsecure_short}} instance name, {{site.data.keyword.appconfig_short}} CRN, trusted profile ID from [Step 1](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-cli-step1), and {{site.data.keyword.cloud_notm}} account ID:

```sh
ibmcloud resource service-instance-update "<workload-protection-instance-name>" -p '{"enable_cspm": true, "target_accounts": [{"account_id": "<ibm-cloud-account-id>", "config_crn": "<app-config-aggregator-CRN>", "trusted_profile_id": "<ibmcspm-tp-wp-app-config-ID>", "delete": true}]}' -g Default
```
{: pre}

This is the same command you used to [connect your {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.sysdigsecure_short}}](#cspm-implement-cli-step5). The only difference is the addition of `"delete": true`.
{: note}

## Verifying compliance scan results
{: #cspm-implement-verify-implementation}

After enabling CSPM, verify that compliance scanning is working correctly.

1. In your {{site.data.keyword.sysdigsecure_short}} instance, click **Sources**, then select **{{site.data.keyword.cloud_notm}} Account**. Your account should display an `Active` status. The status might take a few minutes to update.
2. Click **Open dashboard**. Your account is listed under **Integrations > Environments > {{site.data.keyword.cloud_notm}}**.
3. Click **Inventory** to view your {{site.data.keyword.cloud_notm}} resources. Use the predefined filters or search box to find specific resource types or names. Click any resource to view its configuration, the compliance controls applied to it, and the evaluation results.
4. Click **Posture > Compliance** to review compliance results for available frameworks, such as the {{site.data.keyword.cloud_notm}} Framework for Financial Services. -->
