---

copyright:
  years:  2024
lastupdated: "2024-07-01"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Implementing CSPM (Cloud Security Posture Management) for {{site.data.keyword.cloud_notm}} using the UI and CLI
{: #cspm-implement}

The compliance module in {{site.data.keyword.sysdigsecure_full}} maintains a detailed inventory of resources, enabling prioritization based on full context, and facilitating the resolution of posture misconfigurations. The compliance module supports cloud and Kubernetes Security Posture Management (CSPM and KSPM, respectively) across hybrid cloud environments.

{{site.data.keyword.sysdigsecure_short}} CSPN and KSPM provide compliance and configuration management of resources and critical workloads. Several predefined policies are supported, including {{site.data.keyword.cloud_notm}} Framework for Financial Services, Digital Operational Resilience Act (DORA) or CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark to achieve security and compliance for your environment. Custom policies are also supported.

The {{site.data.keyword.cloud_notm}} CSPM feature in {{site.data.keyword.sysdigsecure_short}} interacts with {{site.data.keyword.appconfig_short}} for gathering all your resource configuration details. The integration uses {{site.data.keyword.IBM_notm}} [IAM trusted profiles](/docs/account?topic=account-create-trusted-profile&interface=ui) for managing permissions. 

You can easily integrate {{site.data.keyword.cloud_notm}} accounts to implement CSPM for new and for existing {{site.data.keyword.sysdigsecure_short}} instances.

## Before you begin
{: #cspm-implement-prereqs}

Before you get started, you have the following requirements:

- You have at least assigned the `Manager` role for the [{{site.data.keyword.appconfig_short}} service](/docs/app-configuration?topic=app-configuration-ac-service-access-management). This is required to enable service configuration reading that is required for {{site.data.keyword.cloud_notm}} CSPM.
- You already have a {{site.data.keyword.sysdigsecure_short}} instance or enough permissions to create a new instance.
- Permissions to create and manage trusted profiles.

## Integrating to an existing {{site.data.keyword.sysdigsecure_short}} instance using the UI
{: #cspm-implement-ui-existing}
{: ui}

To enable CSPM for your {{site.data.keyword.cloud_notm}} account from your existing {{site.data.keyword.sysdigsecure_short}} instance, follow the next steps:

1. Go to the **Resource list** and select your {{site.data.keyword.sysdigsecure_short}} instance. You can find your {{site.data.keyword.sysdigsecure_short}} instances under the **Security** section.
2. Select **Sources** and go to the **IBM Cloud Account** tab.
3. In this tab, click on **Add**. Introduce the trusted profile name, {{site.data.keyword.appconfig_short}} name, and plan you would like to use.
4. Finally, click on **Add** to have CSPM on your {{site.data.keyword.cloud_notm}} account. 

Once you provision your instance, results are displayed a few minutes after the connection is established, varying by the scale of the resources.

## Integrating to a new {{site.data.keyword.sysdigsecure_short}} instance via UI
{: #cspm-implement-ui-new}
{: ui}

To enable CSPM for your {{site.data.keyword.cloud_notm}} account when provisioning a new {{site.data.keyword.sysdigsecure_short}} instance via {{site.data.keyword.cloud_notm}} catalog, set the **Enable Cloud Security Posture Management (CSPM) for your IBM Cloud account** switch to on.

1. Select the trusted profile name that will be used for connecting to {{site.data.keyword.appconfig_short}} service and collecting resource definitions for running the posture validations.
2. Select the {{site.data.keyword.appconfig_short}} instance name and plan. By default the **Basic** plan is selected.

Once you provision your instance, results are displayed about 5-10 minutes after the connection, varying by the scale of the resources.

## Disabling CSPM for {{site.data.keyword.cloud_notm}} via UI
{: #cspm-implement-ui-disable}
{: ui}

To disable CSPM for your {{site.data.keyword.cloud_notm}} account, follow the next steps:

1. Go to the **Resource list** and select your {{site.data.keyword.sysdigsecure_short}} instance. You can find all {{site.data.keyword.sysdigsecure_short}} instances under the **Security** section.
2. Select **Sources** and go to the **IBM Cloud Account** tab.
3. Click on the three dots of the account you want to disable and click **Remove**. 

Your account will be disabled for CSPM in the selected {{site.data.keyword.sysdigsecure_short}} instance.

## Integrating your account using the CLI
{: #cspm-implement-cli}
{: cli}

This section describes the steps you need to perform with the CLI and API in order to manually onboard an {{site.data.keyword.cloud_notm}} account into {{site.data.keyword.sysdigsecure_short}} for implementing CSPM.

You can use the steps described here to also integrate a different {{site.data.keyword.cloud_notm}} account than the one where you have your {{site.data.keyword.sysdigsecure_short}} instance.

Before you begin:
- You need to have an {{site.data.keyword.sysdigsecure_short}} instance. If you don't have one, create one as described in [Provisioning an instance](/docs/workload-protection?topic=workload-protection-provision).
- Get your {{site.data.keyword.sysdigsecure_short}} CRN. You can get this by going to the **Resource list** and clicking the service that you're targeting. In the **Details** section, copy the CRN. It will be referenced in this section as `workload-protection-instance-crn`. 
- Get your {{site.data.keyword.sysdigsecure_short}} Name. You can get this by going to the **Resource list** and clicking the service that you're targeting. In the Details section, copy the **Name**. It will be referenced in this section as `workload-protection-instance-name`. 
- Make sure you have the correct permissions to create trusted profiles, {{site.data.keyword.appconfig_short}} and {{site.data.keyword.sysdigsecure_short}} instances:
  - Account owner.
  - Administrator role on all account management services.
  - Administrator role on the IAM Identity Service. For more information, see [IAM Identity service](/docs/account?topic=account-account-services#identity-service-account-management).
- [Installion of the {{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli). If the CLI is installed, continue with the next step.
- Log in to the {{site.data.keyword.cloud_notm}} account and region where you want to provision the instances. Run the following command: [`ibmcloud login`](https://cloud.ibm.com/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).

This integration requires the following four steps:
1. Create a trusted profile between {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.appconfig_short}}.
2. Create {{site.data.keyword.appconfig_short}} instance.
3. Create a trusted profile for {{site.data.keyword.appconfig_short}} to collect resource configuration.
4. Configure the {{site.data.keyword.appconfig_short}} instance for collecting service configurations.
5. Onboard your {{site.data.keyword.cloud_notm}} account to your {{site.data.keyword.sysdigsecure_short}} instance.

### Step 1: create a trusted profile for {{site.data.keyword.sysdigsecure_short}} interaction with {{site.data.keyword.appconfig_short}}
{: #cspm-implement-cli-step1}
{: cli}

In this step, your {{site.data.keyword.sysdigsecure_short}} instance must already have been created. The {{site.data.keyword.sysdigsecure_short}} instance CRN is used for creating and configuring the trusted profile to interact with {{site.data.keyword.appconfig_short}}.

- It requires the following access policies:
  - Enterprise (`Viewer` + `Usage Report Viewer`) for validating the type of account.
  - {{site.data.keyword.appconfig_short}} (`Manager` + `Configuration Aggregator Reader`)
- CRN (Trust Relationship – {{site.data.keyword.cloud_notm}} Services) is the{{site.data.keyword.sysdigsecure_short}} CRN
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

Create the policy for the trusted profile for enterprise:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-wp-app-config -r Viewer,"Usage Report Viewer" --service-name enterprise
```
{: pre}

Create the Policy for the trusted profile for {{site.data.keyword.appconfig_short}}:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-wp-app-config -r Manager,"Configuration Aggregator Reader" --service-name apprapp
```
{: pre}

### Step 2: create {{site.data.keyword.appconfig_short}} instance
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

### Step 3: trusted profile for {{site.data.keyword.appconfig_short}} for collecting service configuration
{: #cspm-implement-cli-step3}
{: cli}

In this step, you'll be creating the trusted profile that your {{site.data.keyword.appconfig_short}} instance uses to collect all service configurations to perform {{site.data.keyword.cloud_notm}} CSPM. Make sure you have the {{site.data.keyword.appconfig_short}} CRN (`app-config-aggregator-CRN`) you created in Step 2.

To configure correctly the trusted profile, we need the previous step because we use the {{site.data.keyword.appconfig_short}} instance CRN.

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

Create the Policy for the trusted profile for enterprise:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-app-config-aggregator -r Viewer,"Service Configuration Reader" --service-name "All Account Management services"
```
{: pre}

Create the Policy for the trusted profile for {{site.data.keyword.appconfig_short}}:

```sh
ibmcloud iam trusted-profile-policy-create ibmcspm-app-config-aggregator -r Viewer,"Service Configuration Reader" --service-name "All Identity and Access enabled services"
```
{: pre}

### Step 4: configure the {{site.data.keyword.appconfig_short}} instance for collecting service configurations
{: #cspm-implement-cli-step4}
{: cli}

In this step, you configure {{site.data.keyword.appconfig_short}} to start collecting your service configuration. Before starting this step, make sure you have:
- The {{site.data.keyword.appconfig_short}} GUID (`app-config-aggregator-ID`) you created in [Step 2](#cspm-implement-cli-step2).
- The trusted profile for {{site.data.keyword.appconfig_short}} for collecting service configuration (`ibmcspm-tp-app-config-aggregator-ID`) that you created in [Step 3](#cspm-implement-cli-step3).

For this following action, we need to perform a HTTP `PUT` request. We are using `curl` to perform the request.

First, get your IAM API token by running the following command:

```sh
export AUTH_TOKEN=`ibmcloud iam oauth-tokens | awk '{print $4}'`
```
{: pre}

This command stores your token in the variable `AUTH_TOKEN`. For more information, see [Getting the IAM API token](/docs/monitoring?topic=monitoring-api_token#api_iam_token_get).

Now, run the following HTTP `PUT` request to your {{site.data.keyword.appconfig_short}} instance. Remember to replace `<app-config-aggregator-ID>` with your {{site.data.keyword.appconfig_short}} instance ID, `<region>` with the region where you have created your {{site.data.keyword.appconfig_short}} instance:

```sh
curl -X PUT -H "Authorization: Bearer $AUTH_TOKEN" https://<region>.apprapp.cloud.ibm.com/apprapp/config-aggregator/v1/instances/<app-config-aggregator-ID>/settings -d '{"resource_collection_enabled": true, "trusted_profile_id": "<ibmcspm-tp-app-config-aggregator-ID>", "regions": ["all"]}'
```
{: pre}

You should receive the output with the configuration you have set, similar to:

```sh
{"additional_scope":[],"last_updated":"2024-06-20T15:17:15Z","regions":["all"],"resource_collection_enabled":true,"trusted_profile_id":"<ibmcspm-tp-app-config-aggregator-ID>"}
```
{: pre}

### Step 5: onboard your {{site.data.keyword.cloud_notm}} account to your {{site.data.keyword.sysdigsecure_short}} instance
{: #cspm-implement-cli-step5}
{: cli}

In this final step, you configure your {{site.data.keyword.sysdigsecure_short}} instance you need to use the following values from previous steps:
- Your {{site.data.keyword.sysdigsecure_short}} instance name (`workload-protection-instance-name`).
- The {{site.data.keyword.appconfig_short}} CRN (`app-config-aggregator-CRN`) that you created in [Step 2](#cspm-implement-cli-step2).
- The trusted profile for {{site.data.keyword.sysdigsecure_short}} to interact with {{site.data.keyword.appconfig_short}} (`ibmcspm-tp-wp-app-config-ID`) you created in [Step 1](#cspm-implement-cli-step1).
- Your {{site.data.keyword.cloud_notm}} account ID (`<ibm-cloud-account-id>`). You can get it under **Manage > Account > Account Settings** in `ID`.

Run the following CLI command to update your {{site.data.keyword.sysdigsecure_short}} instance to onboard your {{site.data.keyword.cloud_notm}} Account. Replace `<workload-protection-instance-name>` by your {{site.data.keyword.sysdigsecure_short}} instance name, `<app-config-aggregator-CRN>` by your {{site.data.keyword.appconfig_short}} instance CRN and `<ibmcspm-tp-wp-app-config-ID>` by the trusted profile ID created in [Step 2](#cspm-implement-cli-step2) and `<ibm-cloud-account-id>` by your {{site.data.keyword.cloud_notm}} account ID.

```sh
ibmcloud resource service-instance-update "<workload-protection-instance-name>" -p '{"enable_cspm": true, "target_accounts": [{"account_id": "<ibm-cloud-account-id>", "config_crn": "<app-config-aggregator-CRN>", "trusted_profile_id": "<ibmcspm-tp-wp-app-config-ID>"}]}' -g Default
```
{: pre}

## Verifying CSPM implementation
{: #cspm-implement-verify-implementation}

Verifying the integration by following the next steps: 
- In your {{site.data.keyword.sysdigsecure_short}} instance, select **Sources / {{site.data.keyword.cloud_notm}} Account**. You should see your {{site.data.keyword.cloud_notm}} account with the `Active` status. The status can take a few minutes to be updated.
- Access to your {{site.data.keyword.sysdigsecure_short}} instance by clicking in **Open dashboard**, your account will be listed under **Integrations / Cloud Accounts**. 
- In your {{site.data.keyword.sysdigsecure_short}}, access **Inventory** and review the list of {{site.data.keyword.cloud_notm}} resources of your account. You have available many predefined filters you can use or the search box to filter by resource type or resource name. By clicking in each resource, you can review the resource configuration, the Posture controls applied against it and the results of the evaluation.
- By accessing to **Posture / Compliance**, you can review the results of the available frameworks (such as {{site.data.keyword.cloud_notm}} Framework for Financial Services) of your {{site.data.keyword.cloud_notm}} resources.

## Disabling CSPM for {{site.data.keyword.cloud_notm}} with the CLI
{: #cspm-implement-disable}
{: cli}

In order to disable CSPM for your account, you need to run the following command. Replace `<workload-protection-instance-name>` by your {{site.data.keyword.sysdigsecure_short}} instance name, `<app-config-aggregator-CRN>` by your {{site.data.keyword.appconfig_short}} instance CRN and `<ibmcspm-tp-wp-app-config-ID>` by the trusted profile ID created in [Step 2](#cspm-implement-cli-step2) and `<ibm-cloud-account-id>` by your {{site.data.keyword.cloud_notm}} account ID:

```sh
ibmcloud resource service-instance-update "<workload-protection-instance-name>" -p '{"enable_cspm": true, "target_accounts": [{"account_id": "<ibm-cloud-account-id>", "config_crn": "<app-config-aggregator-CRN>", "trusted_profile_id": "<ibmcspm-tp-wp-app-config-ID>", "delete": true}]}' -g Default
```
{: pre}

This is the same command described in [Step 5](#cspm-implement-cli-step5) with the addition of `"delete": true`.
{: note}