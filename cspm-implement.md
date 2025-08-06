---

copyright:
  years:  2024
lastupdated: "2025-07-31"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Implementing CSPM (Cloud Security Posture Management) for {{site.data.keyword.cloud_notm}}
{: #cspm-implement}

The compliance module in {{site.data.keyword.sysdigsecure_full}} maintains a detailed inventory of resources, enabling prioritization based on full context, and facilitating the resolution of posture misconfigurations. The compliance module supports cloud and Kubernetes Security Posture Management (CSPM and KSPM, respectively) across hybrid cloud environments.

{{site.data.keyword.sysdigsecure_short}} CSPM and KSPM provide compliance and configuration management of resources and critical workloads. Several predefined policies are supported, including {{site.data.keyword.cloud_notm}} Framework for Financial Services, Digital Operational Resilience Act (DORA) or CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark to achieve security and compliance for your environment. Custom policies are also supported.

The {{site.data.keyword.cloud_notm}} CSPM feature in {{site.data.keyword.sysdigsecure_short}} interacts with the aggregator feature of {{site.data.keyword.appconfig_short}} for gathering all your resource configuration details. The aggregator feature is free of charge and part of the Basic plan of {{site.data.keyword.appconfig_short}}. The integration uses {{site.data.keyword.IBM_notm}} [IAM trusted profiles](/docs/account?topic=account-create-trusted-profile&interface=ui) for managing permissions. 

You can easily integrate {{site.data.keyword.cloud_notm}} accounts to implement CSPM for new and for existing {{site.data.keyword.sysdigsecure_short}} instances.

You can also integrate your {{site.data.keyword.cloud_notm}} Enterprise to implement CSPM for all the accounts that belong to your organization. All steps to integrate your Enterprise are described in this [documentation](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-enterprise).

## Before you begin
{: #cspm-implement-prereqs}

Before you get started, make sure you have the following requirements completed:

- You have assigned at least the `Manager` role to the [{{site.data.keyword.appconfig_short}} service](/docs/app-configuration?topic=app-configuration-ac-service-access-management). This is required for the CSPM to enable service configuration.
- You already have a {{site.data.keyword.sysdigsecure_short}} instance or enough permissions to create a new instance.
- [Permissions to create and manage trusted profiles](/docs/account?topic=account-create-trusted-profile&interface=ui#tp-roles-reqs).

When context-based restrictions are enabled for any resource in your {{site.data.keyword.cloud_notm}} account, configuration cannot be collected unless access to that resource is provided. To provide access, you need to create a rule. When asked to add a context, create a network zone and [select App Configuration as the reference service](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator#ac-configuration-aggregator-with-workload-protection). 
{: note}

## Integrating with an existing {{site.data.keyword.sysdigsecure_short}} instance
{: #cspm-implement-ui-existing}
{: ui}

To enable CSPM for your {{site.data.keyword.cloud_notm}} account from your existing {{site.data.keyword.sysdigsecure_short}} instance, follow the next steps:

1. Go to the **Resource list** and select your {{site.data.keyword.sysdigsecure_short}} instance. You can find your {{site.data.keyword.sysdigsecure_short}} instances under the **Security** section.
2. Select **Sources** and go to the **IBM Cloud Account** tab.
3. In this tab, click on **Add**. Introduce the trusted profile name, {{site.data.keyword.appconfig_short}} name, and select the plan.
4. Finally, click on **Add** to have CSPM on your {{site.data.keyword.cloud_notm}} account. 

Once you provision your instance, results are displayed a few minutes after the connection is established, depending on the number of resources.

## Integrating to a new {{site.data.keyword.sysdigsecure_short}} instance
{: #cspm-implement-ui-new}
{: ui}

To enable CSPM for your {{site.data.keyword.cloud_notm}} account when provisioning a new {{site.data.keyword.sysdigsecure_short}} instance via {{site.data.keyword.cloud_notm}} catalog, set the **Enable Cloud Security Posture Management (CSPM) for your IBM Cloud account** switch to on.

1. Select the trusted profile name that will be used for connecting to {{site.data.keyword.appconfig_short}} service and collecting resource definitions for running the posture validations.
2. Select the {{site.data.keyword.appconfig_short}} instance name and plan. By default the **Basic** plan is selected.

Once you provision your instance, results are displayed about 5-10 minutes after the connection, depeding on the number of resources.

## Disabling CSPM on the {{site.data.keyword.cloud_notm}} account
{: #cspm-implement-ui-disable}
{: ui}

To disable CSPM for your {{site.data.keyword.cloud_notm}} account, follow the next steps:

1. Go to the **Resource list** and select your {{site.data.keyword.sysdigsecure_short}} instance. You can find all {{site.data.keyword.sysdigsecure_short}} instances under the **Security** section.
2. Select **Sources** and go to the **IBM Cloud Account** tab.
3. Click on the three dots of the account you want to disable and click **Remove**. 

Your account will be disabled for CSPM in the selected {{site.data.keyword.sysdigsecure_short}} instance.

## Integrating your account
{: #cspm-implement-cli}
{: cli}

This section describes the steps you need to perform with the CLI and API in order to manually onboard an {{site.data.keyword.cloud_notm}} account onto {{site.data.keyword.sysdigsecure_short}} for implementing CSPM.

You can use the steps described here to also integrate a different {{site.data.keyword.cloud_notm}} account than the one where you have your {{site.data.keyword.sysdigsecure_short}} instance.

Before you begin:
- You need to have a {{site.data.keyword.sysdigsecure_short}} instance. If you don't have one, create one as described in [Provisioning an instance](/docs/workload-protection?topic=workload-protection-provision).
- Get your {{site.data.keyword.sysdigsecure_short}} CRN. You can get this by going to the **Resource list** and clicking the service that you're targeting. In the **Details** section, copy the CRN. It will be referenced in this section as `workload-protection-instance-crn`. 
- Get your {{site.data.keyword.sysdigsecure_short}} name. You can get this by going to the **Resource list** and clicking the service that you're targeting. In the Details section, copy the **Name**. It will be referenced in this section as `workload-protection-instance-name`. 
- Make sure you have the correct permissions to create trusted profiles, {{site.data.keyword.appconfig_short}} and {{site.data.keyword.sysdigsecure_short}} instances:
  - Account owner.
  - Administrator role on all account management services.
  - Administrator role on the IAM Identity Service. For more information, see [IAM Identity service](/docs/account?topic=account-account-services#identity-service-account-management).
- [Installion of the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli). If the CLI is installed, continue with the next step.
- Log in to the {{site.data.keyword.cloud_notm}} account and region where you want to provision the instances. Run the following command: [`ibmcloud login`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).

This integration requires the following four steps:
1. Create a trusted profile between {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.appconfig_short}}.
2. Create {{site.data.keyword.appconfig_short}} instance.
3. Create a trusted profile for {{site.data.keyword.appconfig_short}} to collect resource configuration.
4. Configure the {{site.data.keyword.appconfig_short}} instance for collecting service configurations.
5. Onboard your {{site.data.keyword.cloud_notm}} account to your {{site.data.keyword.sysdigsecure_short}} instance.

### Step 1: Create a trusted profile for {{site.data.keyword.sysdigsecure_short}} interaction with {{site.data.keyword.appconfig_short}}
{: #cspm-implement-cli-step1}
{: cli}

Before this step, your {{site.data.keyword.sysdigsecure_short}} instance must already have been created. The {{site.data.keyword.sysdigsecure_short}} instance CRN is used for creating and configuring the trusted profile to interact with {{site.data.keyword.appconfig_short}}.

- It requires the following access policies:
  - Enterprise account (`Viewer` + `Usage Report Viewer`) for validating the type of account.
  - {{site.data.keyword.appconfig_short}} (`Manager` + `Configuration Aggregator Reader`)
- CRN (Trust Relationship – {{site.data.keyword.cloud_notm}} Services) is the {{site.data.keyword.sysdigsecure_short}} CRN
  - For example: `crn:v1:bluemix:public:sysdig-secure:us-south:a/1560be5426584bf8a43e75xxxxxxxxxx:299e4ca4-d96c-4fba-9691-xxxxxxxx::` 

You can create this trusted profile with the following CLI commands:

Create the trusted profile (you can modify the name). **Save the `ID` to be used later. It will be referenced later as `ibmcspm-tp-wp-app-config-ID`**:

```sh
ibmcloud iam trusted-profile-create ibmcspm-wp-app-config --description "Trusted profile for Workload Protection interaction with Config Service"
```
{: pre}

Assign the corresponding trust relationship. Replace `workload-protection-instance-crn` with your {{site.data.keyword.sysdigsecure_short}} CRN:

```sh
ibmcloud iam trusted-profile-identity-create ibmcspm-wp-app-config --id workload-protection-instance-crn --id-type CRN
```
{: pre}

Create the policy for the trusted profile for the enterprise account:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-wp-app-config -r Viewer,"Usage Report Viewer" --service-name enterprise
```
{: pre}

Create the Policy for the trusted profile for {{site.data.keyword.appconfig_short}}:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-wp-app-config -r Manager,"Configuration Aggregator Reader" --service-name apprapp
```
{: pre}

### Step 2: Create {{site.data.keyword.appconfig_short}} instance
{: #cspm-implement-cli-step2}
{: cli}

In this step, you'll be creating an {{site.data.keyword.appconfig_short}} instance that your {{site.data.keyword.sysdigsecure_short}} will use for collecting all resource definitions to implement the {{site.data.keyword.cloud_notm}} CSPM.

You can create a new {{site.data.keyword.appconfig_short}} instance with the following CLI command. You can change the plan, region or resource group. See this [doc](/docs/app-configuration?topic=app-configuration-ac-create-an-instance) for more information. 

Save the `CRN` and the `GUID` to be used later. It will be referenced later as `app-config-aggregator-CRN` and `app-config-aggregator-ID` respectively.
{: tip}

Run the following command to create the {{site.data.keyword.appconfig_short}} instance. Replace the plan, region or resource group based on your needs:

```sh
ibmcloud resource service-instance-create "ibmcspm-app-config" "apprapp" "basic" "us-south" -g Default
```
{: pre}

Note that the CRN (`ID` from the output) is referenced as `app-config-aggregator-CRN`. Likewise, instance ID (`GUID` from the output) is referenced as `app-config-aggregator-ID`. Save those values as they will be used in the following steps.
{: important}

### Step 3: Trusted profile for {{site.data.keyword.appconfig_short}} for collecting service configuration
{: #cspm-implement-cli-step3}
{: cli}

In this step, you'll be creating the trusted profile that your {{site.data.keyword.appconfig_short}} instance uses to collect all service configurations to perform {{site.data.keyword.cloud_notm}} CSPM. Make sure you have the {{site.data.keyword.appconfig_short}} CRN (`app-config-aggregator-CRN`) you created in Step 2.

To configure the trusted profile correctly, you need the {{site.data.keyword.appconfig_short}} instance CRN from the previous step.

- It requires the following Access Policies:
  - All Account Management services (`Viewer` + `Service Configuration Reader`)
  - All Identity and Access enabled services (`Reader` + `Viewer` + `Service Configuration Reader`)
- CRN (Trust Relationship – {{site.data.keyword.cloud_notm}} Services) to the Config Service CRN
  - For example: `crn:v1:bluemix:public:apprapp:us-south:a/1560be5426584bf8a43e75xxxxxxxxxx:b4829f20-6d22-4604-939d-xxxxxxxx::`

You can create this trusted profile with the following CLI commands:

Create the trusted profile (you can modify the name). Note: save the `ID` to be used later. It will be referenced later as `ibmcspm-tp-app-config-aggregator-ID`:

```sh
ibmcloud iam trusted-profile-create ibmcspm-app-config-aggregator --description "Trusted profile for App Configuration for collecting service configuration"
```
{: pre}

Assign the corresponding Trust Relationship. Replace `app-config-aggregator-CRN` with your {{site.data.keyword.sysdigsecure_short}} CRN:

```sh
ibmcloud iam trusted-profile-identity-create ibmcspm-app-config-aggregator --id app-config-aggregator-CRN --id-type CRN
```
{: pre}

Create the Policy for the trusted profile for the enterprise account:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-app-config-aggregator -r Viewer,"Service Configuration Reader" --service-name "All Account Management services"
```
{: pre}

Create the Policy for the trusted profile for {{site.data.keyword.appconfig_short}}:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-app-config-aggregator -r Viewer,"Service Configuration Reader" --service-name "All Identity and Access enabled services"
```
{: pre}

### Step 4: Configure the {{site.data.keyword.appconfig_short}} instance for collecting service configurations
{: #cspm-implement-cli-step4}
{: cli}

In this step, you configure {{site.data.keyword.appconfig_short}} to start collecting your service configuration. You can perform this step by going to your {{site.data.keyword.appconfig_short}} instance and [enable Configuration Aggregator](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator#ac-enable-configuration-aggregator-single-account).

You can also perform this step via API. Before starting this step, make sure you have:
- The {{site.data.keyword.appconfig_short}} GUID (`app-config-aggregator-ID`) you created in [Step 2](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-cli-step2).
- The trusted profile for {{site.data.keyword.appconfig_short}} for collecting service configuration (`ibmcspm-tp-app-config-aggregator-ID`) that you created in [Step 3](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-cli-step3).

For the following action, run an HTTP `PUT` request using `curl`.

First, get your IAM API token by running the following command:

```sh
export AUTH_TOKEN=`ibmcloud iam oauth-tokens | awk '{print $4}'`
```
{: pre}

This command stores your token in the variable `AUTH_TOKEN`. For more information, see [Getting the IAM API token](/docs/monitoring?topic=monitoring-api_token#api_iam_token_get).

Now, run the following HTTP `PUT` request to your {{site.data.keyword.appconfig_short}} instance. Remember to replace `<app-config-aggregator-ID>` with your {{site.data.keyword.appconfig_short}} instance ID, `<region>` with the region where you have created your {{site.data.keyword.appconfig_short}} instance:

```sh
curl -X PUT -H "Authorization: Bearer $AUTH_TOKEN" https://<region>.apprapp.cloud.ibm.com/apprapp/config_aggregator/v1/instances/<app-config-aggregator-ID>/settings -d '{"resource_collection_enabled": true, "trusted_profile_id": "<ibmcspm-tp-app-config-aggregator-ID>", "regions": ["all"]}'
```
{: pre}

You should receive the output with the configuration you have set, similar to:

```sh
{"additional_scope":[],"last_updated":"2024-06-20T15:17:15Z","regions":["all"],"resource_collection_enabled":true,"trusted_profile_id":"<ibmcspm-tp-app-config-aggregator-ID>"}
```
{: pre}

### Step 5: Onboard your {{site.data.keyword.cloud_notm}} account to your {{site.data.keyword.sysdigsecure_short}} instance
{: #cspm-implement-cli-step5}
{: cli}

In this final step, you configure your {{site.data.keyword.sysdigsecure_short}} instance you need to use the following values from previous steps:
- Your {{site.data.keyword.sysdigsecure_short}} instance name (`workload-protection-instance-name`).
- The {{site.data.keyword.appconfig_short}} CRN (`app-config-aggregator-CRN`) that you created in [Step 2](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-cli-step2).
- The trusted profile for {{site.data.keyword.sysdigsecure_short}} to interact with {{site.data.keyword.appconfig_short}} (`ibmcspm-tp-wp-app-config-ID`) you created in [Step 1](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-cli-step1).
- Your {{site.data.keyword.cloud_notm}} account ID (`<ibm-cloud-account-id>`). You can get it under **Manage > Account > Account Settings** in `ID`.

If previously you have onboarded any other {{site.data.keyword.cloud_notm}} account or add any other parameter, make sure to keep existing parameters. You can see the existing used paramaters of your instance by running `ibmcloud resource service-instance <workload-protection-instance-name> --output json` replacing `<workload-protection-instance-name>` by your {{site.data.keyword.sysdigsecure_short}} instance name.
{: note}

Run the following CLI command to update your {{site.data.keyword.sysdigsecure_short}} instance to onboard your {{site.data.keyword.cloud_notm}} Account. Replace `<workload-protection-instance-name>` by your {{site.data.keyword.sysdigsecure_short}} instance name, `<app-config-aggregator-CRN>` by your {{site.data.keyword.appconfig_short}} instance CRN and `<ibmcspm-tp-wp-app-config-ID>` by the trusted profile ID created in [Step 2](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-cli-step2) and `<ibm-cloud-account-id>` by your {{site.data.keyword.cloud_notm}} account ID.

```sh
ibmcloud resource service-instance-update "<workload-protection-instance-name>" -p '{"enable_cspm": true, "target_accounts": [{"account_id": "<ibm-cloud-account-id>", "config_crn": "<app-config-aggregator-CRN>", "trusted_profile_id": "<ibmcspm-tp-wp-app-config-ID>"}]}' -g Default
```
{: pre}

## Verifying CSPM implementation
{: #cspm-implement-verify-implementation}

Verifying the integration by following the next steps: 
- In your {{site.data.keyword.sysdigsecure_short}} instance, select **Sources / {{site.data.keyword.cloud_notm}} Account**. You should see your {{site.data.keyword.cloud_notm}} account with the `Active` status. The status can take a few minutes to be updated.
- Access to your {{site.data.keyword.sysdigsecure_short}} instance by clicking in **Open dashboard**, your account will be listed under **Integrations / Cloud Accounts**. 
- In your {{site.data.keyword.sysdigsecure_short}}, access **Inventory** and review the list of {{site.data.keyword.cloud_notm}} resources of your account. You have many predefined filters available that you can choose from. Alternatively, you can use the search box to filter by resource type or resource name. By clicking in each resource, you can review the resource configuration, the posture controls applied against it and the results of the evaluation.
- By accessing **Posture / Compliance**, you can review the results of the available frameworks (such as {{site.data.keyword.cloud_notm}} Framework for Financial Services) of your {{site.data.keyword.cloud_notm}} resources.

## Disabling CSPM for {{site.data.keyword.cloud_notm}} with the CLI
{: #cspm-implement-disable}
{: cli}

In order to disable CSPM for your account, you need to run the following command. Replace `<workload-protection-instance-name>` by your {{site.data.keyword.sysdigsecure_short}} instance name, `<app-config-aggregator-CRN>` by your {{site.data.keyword.appconfig_short}} instance CRN and `<ibmcspm-tp-wp-app-config-ID>` by the trusted profile ID created in [Step 2](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-cli-step2) and `<ibm-cloud-account-id>` by your {{site.data.keyword.cloud_notm}} account ID:

```sh
ibmcloud resource service-instance-update "<workload-protection-instance-name>" -p '{"enable_cspm": true, "target_accounts": [{"account_id": "<ibm-cloud-account-id>", "config_crn": "<app-config-aggregator-CRN>", "trusted_profile_id": "<ibmcspm-tp-wp-app-config-ID>", "delete": true}]}' -g Default
```
{: pre}

This is the same command described in [Step 5](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-cli-step5) with the addition of `"delete": true`.
{: note}

## Integrating your Enterprise
{: #cspm-implement-enterprise}
{: cli}

This section describes the steps you need to perform with the CLI in order to onboard an {{site.data.keyword.cloud_notm}} Enterprise onto {{site.data.keyword.sysdigsecure_short}} for implementing CSPM. These steps will integrate all your child accounts and the Enterprise management account.

Before you get started, make sure you have the following requirements completed to connect an {{site.data.keyword.sysdigsecure_short}} Enterprise for CSPM:

- [Permissions to create Trusted profiles templates, policies and assignments](/docs/enterprise-management?topic=enterprise-management-tp-template-create&interface=ui#before-you-tp-template).
- You have assigned at least the `Manager` role to the [{{site.data.keyword.appconfig_short}} service](/docs/app-configuration?topic=app-configuration-ac-service-access-management). This is required for the CSPM to enable service configuration.
- You already have a {{site.data.keyword.sysdigsecure_short}} instance or enough permissions to create a new instance.
- [Permissions to create and manage trusted profiles](/docs/account?topic=account-create-trusted-profile&interface=ui#tp-roles-reqs).

This integration requires the following four steps:
1. Create a trusted profile between {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.appconfig_short}}.
2. Create {{site.data.keyword.appconfig_short}} instance
3. Configure the {{site.data.keyword.appconfig_short}} instance for collecting service configurations from the entire Enterprise.
4. Onboard your {{site.data.keyword.cloud_notm}} Enterprise to your {{site.data.keyword.sysdigsecure_short}} instance.

### Step 1: Create a trusted profile for {{site.data.keyword.sysdigsecure_short}} interaction with {{site.data.keyword.appconfig_short}}
{: #cspm-implement-enterprise-step1}
{: cli}

Before this step, your {{site.data.keyword.sysdigsecure_short}} instance must already have been created. The {{site.data.keyword.sysdigsecure_short}} instance CRN is used for creating and configuring the trusted profile to interact with {{site.data.keyword.appconfig_short}}.

- It requires the following access policies:
  - Enterprise account (`Viewer` + `Usage Report Viewer`) for validating the type of account.
  - {{site.data.keyword.appconfig_short}} (`Manager` + `Configuration Aggregator Reader`)
- CRN (Trust Relationship – {{site.data.keyword.cloud_notm}} Services) is the {{site.data.keyword.sysdigsecure_short}} CRN
  - For example: `crn:v1:bluemix:public:sysdig-secure:us-south:a/1560be5426584bf8a43e75xxxxxxxxxx:299e4ca4-d96c-4fba-9691-xxxxxxxx::` 

You can create this trusted profile with the following CLI commands:

Create the trusted profile (you can modify the name). **Save the `ID` to be used later. It will be referenced later as `ibmcspm-tp-wp-app-config-ID`**:

```sh
ibmcloud iam trusted-profile-create ibmcspm-wp-app-config --description "Trusted profile for Workload Protection interaction with Config Service"
```
{: pre}

Assign the corresponding trust relationship. Replace `workload-protection-instance-crn` with your {{site.data.keyword.sysdigsecure_short}} CRN:

```sh
ibmcloud iam trusted-profile-identity-create ibmcspm-wp-app-config --id workload-protection-instance-crn --id-type CRN
```
{: pre}

Create the policy for the trusted profile for the enterprise account:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-wp-app-config -r Viewer,"Usage Report Viewer" --service-name enterprise
```
{: pre}

Create the Policy for the trusted profile for {{site.data.keyword.appconfig_short}}:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-wp-app-config -r Manager,"Configuration Aggregator Reader" --service-name apprapp
```
{: pre}

### Step 2: Create {{site.data.keyword.appconfig_short}} instance
{: #cspm-implement-enterprise-step2}
{: cli}

In this step, you create an {{site.data.keyword.appconfig_short}} instance that your {{site.data.keyword.sysdigsecure_short}} uses for collecting all resource definitions to implement the {{site.data.keyword.cloud_notm}} CSPM.

You can create a new {{site.data.keyword.appconfig_short}} instance with the following CLI command. You can change the plan, region or resource group. See this [doc](/docs/app-configuration?topic=app-configuration-ac-create-an-instance) for more information. 

Save the `CRN` and the `GUID` to be used later. It will be referenced later as `app-config-aggregator-CRN` and `app-config-aggregator-ID` respectively.
{: tip}

Run the following command to create the {{site.data.keyword.appconfig_short}} instance. Replace the plan, region or resource group based on your needs:

```sh
ibmcloud resource service-instance-create "ibmcspm-app-config" "apprapp" "basic" "us-south" -g Default
```
{: pre}

Note that the CRN (`ID` from the output) is referenced as `app-config-aggregator-CRN`. Likewise, instance ID (`GUID` from the output) is referenced as `app-config-aggregator-ID`. Save those values as they will be used in the following steps.
{: important}

### Step 3: Configure the {{site.data.keyword.appconfig_short}} instance for collecting service configurations from the entire Enterprise
{: #cspm-implement-enterprise-step3}
{: cli}

Access to your App Configuration instance in the {{site.data.keyword.cloud_notm}} console. You can find it under the `Resource List` and Developer tools. 

Follow the steps to [Enable Configuration aggregator - Enterprise Account](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator#ac-enable-configuration-aggregator-enterprise-account).

### Step 4: Onboard your {{site.data.keyword.cloud_notm}} Enterprise to your {{site.data.keyword.sysdigsecure_short}} instance
{: #cspm-implement-enterprise-step4}
{: cli}

In this final step, you configure your {{site.data.keyword.sysdigsecure_short}} instance you need to use the following values from previous steps:
- Your {{site.data.keyword.sysdigsecure_short}} instance name (`workload-protection-instance-name`).
- The {{site.data.keyword.appconfig_short}} CRN (`app-config-aggregator-CRN`) that you created in [Step 2](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-enterprise-step2).
- The trusted profile for {{site.data.keyword.sysdigsecure_short}} to interact with {{site.data.keyword.appconfig_short}} (`ibmcspm-tp-wp-app-config-ID`) you created in [Step 1](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-enterprise-step1).

If previously you have onboarded any other {{site.data.keyword.cloud_notm}} account or add any other parameter, make sure to keep existing parameters. You can see the existing used paramaters of your instance by running `ibmcloud resource service-instance <workload-protection-instance-name> --output json` replacing `<workload-protection-instance-name>` by your {{site.data.keyword.sysdigsecure_short}} instance name.
{: note}

Run the following CLI command to update your {{site.data.keyword.sysdigsecure_short}} instance to onboard your {{site.data.keyword.cloud_notm}} Enterprise. Replace `<workload-protection-instance-name>` by your {{site.data.keyword.sysdigsecure_short}} instance name, `<app-config-aggregator-CRN>` by your {{site.data.keyword.appconfig_short}} instance CRN and `<ibmcspm-tp-wp-app-config-ID>` by the trusted profile ID created in [Step 2](/docs/workload-protection?topic=workload-protection-cspm-implement&interface=cli#cspm-implement-enterprise-step2).

```sh
ibmcloud resource service-instance-update "<workload-protection-instance-name>" -p '{"enable_cspm": true, "target_accounts": [{"account_type": "ENTERPRISE", "config_crn": "<app-config-aggregator-CRN>", "trusted_profile_id": "<ibmcspm-tp-wp-app-config-ID>"}]}' -g Default
```
{: pre}
