---

copyright:
  years:  2023
lastupdated: "2023-09-26"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with {{site.data.keyword.sysdigsecure_full_notm}}
{: #getting-started}

In architectures that are focused on container and microservices, you can use {{site.data.keyword.sysdigsecure_full}} to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions, and compliance from source to run.
{: shortdesc}

For more information about how an instance of {{site.data.keyword.sysdigsecure_full_notm}} can be integrated with {{site.data.keyword.compliance_short}} to run scans that validate your level of compliance, check out [Connecting Workload Protection](cloud.ibm.com/docs/security-compliance?topic=security-compliance-setup-workload-protection).
{: tip}


## Before you begin
{: #getting-started-prereqs}

- You must have a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Registration](https://cloud.ibm.com/login){: external}.

- Check the regions where the service is available. [Learn more](/docs/workload-protection?topic=workload-protection-regions). You can complete the steps in any of the supported regions.


## Step 1. Manage user access
{: #getting-started-step1}

Every user that accesses the {{site.data.keyword.sysdigsecure_full_notm}} service in your account must be assigned an access policy with an IAM user role defined. The policy determines the actions that the user can run within the context of the service or instance you selected. The allowable actions are customized and defined as operations that are allowed to be run on the service. The actions are then mapped to IAM user roles. For more information, see [Managing user access in the {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-iam#iam).

When a user is granted permissions in the {{site.data.keyword.cloud_notm}} to work with the {{site.data.keyword.sysdigsecure_full_notm}} service, the user is automatically granted a service role. This role determines the actions that a user has permissions to run. For more information, see [Controlling access through IAM](/docs/workload-protection?topic=workload-protection-iam).

Before you can provision an instance, you need to understand:
* The account owner can create, view, and delete an instance of a service in the {{site.data.keyword.cloud_notm}}, and can grant permissions to other users to work with the {{site.data.keyword.sysdigsecure_full_notm}} service.
* You must have permissions to create resources in the *Default* resource group.
* Other {{site.data.keyword.cloud_notm}} users with `administrator` or `editor` permissions can manage the {{site.data.keyword.sysdigsecure_full_notm}} service in the {{site.data.keyword.cloud_notm}}. These users must also have platform permissions to create resources within the context of the resource group where they plan to provision the instance.

To grant a user the administrator role for the service and to manage instances within a resource group in the account, the user must have an IAM policy for the {{site.data.keyword.sysdigsecure_full_notm}} service. For more information, see [Granting permissions to work with the {{site.data.keyword.sysdigsecure_full_notm}} service](/docs/workload-protection?topic=workload-protection-iam_grant).

By default, users are automatically added as members of the **Secure Operations** team that is predefined for each {{site.data.keyword.sysdigsecure_full_notm}} instance. Users have full permissions to see all the data in the web UI.

An administrator can restrict access to data by managing users in teams and controlling what data is visible. For example, to restrict users being able to view permissions, an administrator can create a default team with limited scope and visibility. Then, manually assign users to other teams. For more information, see [Working with teams](/docs/workload-protection?topic=workload-protection-teams#teams).
{: note}


## Step 2. Provision an instance
{: #getting-started-step2}

To add monitoring features with {{site.data.keyword.sysdigsecure_full_notm}} in the {{site.data.keyword.cloud_notm}}, you must provision an instance of the {{site.data.keyword.sysdigsecure_full_notm}} service.

Instances are provisioned in the context of a resource group. A resource group organizes your services for access control and billing purposes. You can provision the {{site.data.keyword.sysdigsecure_full_notm}} instance in the *default* resource group or in a custom resource group.

To provision an instance through the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

   Open the [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/login){: external}.

   After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Security** category.

4. Click the **{{site.data.keyword.sysdigsecure_full_notm}}** tile.

5. Select the location.

6. Select a service plan.

   For more information about the service plans, see [Service plans](/docs/workload-protection?topic=workload-protection-pricing_plans#pricing_plans).

7. Enter a service name.

8. Select a resource group. By default, the **Default** resource group is set.

9. Click **Create** to provision an instance.

The service UI opens.

To provision an instance through the CLI, see [Provisioning a Monitoring instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/workload-protection?topic=workload-protection-provision#provision_cli).
{: tip}

## Step 3. Connect a data source by configuring an agent
{: #getting-started-secure-step3}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you can deploy the agent on your cluster. The agent collects data that you can use for intrusion detection, posture management, vulnerability scanning, and incident response capabilites.

![Agents that can be configured to provide data to {{site.data.keyword.sysdigsecure_full_notm}}](images/Agent-Collection.svg "Agents that can be configured to provide data to {{site.data.keyword.sysdigsecure_full_notm}}"){: caption="Figure 1. Agents that can be configured to provide data to {{site.data.keyword.sysdigsecure_full_notm}}" caption-side="bottom"}

Choose 1 of the following options:
1. [Configure an agent for Kubernetes](/docs/workload-protection?topic=workload-protection-agent-deploy-kube-helm).
2. [Configire an agent for {{site.data.keyword.redhat_openshift_notm}}](/docs/workload-protection?topic=workload-protection-agent-deploy-openshift-helm).


## Step 4. Launch the web UI
{: #getting-started-step4}

After you provision an instance of the {{site.data.keyword.sysdigsecure_full_notm}} service, and configure a monitoring agent for your node, you can view, monitor, and manage data through the service's web UI.

You launch the web UI within the context of the {{site.data.keyword.sysdigsecure_full_notm}} instance, from the {{site.data.keyword.cloud_notm}} UI.

Complete the following steps to launch the monitoring UI:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

    Click [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/login){: external} to launch the {{site.data.keyword.cloud_notm}} dashboard.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Resource List**.

3. Select **Security**.

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select one instance. Then, click **Open dashboard**.

    The Web UI opens.



## Step 5. Secure your environment
{: #getting-started-secure-step5}

See the following table for tasks that you can run to secure your environment:

| Action                              | Descripion                  |
|-------------------------------------|------------------------------|
| [Integrate scanning into your CI/CD Pipeline](https://docs.sysdig.com/en/docs/sysdig-secure/scanning/integrate-with-cicd-tools/){: external} | You can integrate scanning into your CI/CD Pipeline to analyze images that are available on the CI/CD worker nodes. |
| [Configure a notification channel](/docs/workload-protection?topic=workload-protection-notifications#notifications_create) | You can configure a notification channel to get notified about events, anomalies, or security incidents that require attention. |
| [Scan container images](/docs/workload-protection?topic=workload-protection-scan_kube)             | You can scan container images for vulnerabilities, and other violations.  |
| [Configure an image scanning alert](/docs/workload-protection?topic=workload-protection-alert-config) | You can set up a runtime `Scanning Alert` to detect if an image is impacted by newly discovered vulnerabilities. You can scan a repository that hosts container images for vulnerabilities, secrets, and license violations. Then, you can configure an alert on the repository to receive notifications on issues that need your attention.  |
| [Configure a rule](/docs/workload-protection?topic=workload-protection-manage_rules)                  | You can create a `Detection Rule` to detect and respond to anomalous runtime activity.  \n You can create a rule to specify which image versions can be used. |
| [Define a policy](docs/workload-protection?topic=workload-protection-manage_policies)                     | You can configure a policy on a resource and define what to do when 1 or more rules that are included in the policy are noncompliant.  \n Secure includes a number of pre-defined policies that you can use. |
| [Configure a benchmark task](https://docs.sysdig.com/en/docs/sysdig-secure/posture/compliance/legacy-versions/benchmarks-legacy/configure-benchmark-tasks/){: external}        | You can use [Compliance dashboards and metrics](https://docs.sysdig.com/en/docs/sysdig-secure/home/secure-dashboards/){: external} to monitor the status of your sources based on the benchmark task that you configure.|
{: caption="Table 1. Tasks to secure your environment" caption-side="bottom"}
