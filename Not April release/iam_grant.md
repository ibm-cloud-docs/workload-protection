---

copyright:
  years:  2023
lastupdated: "2023-01-14"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Granting permissions to work with the {{site.data.keyword.sysdigsecure_full_notm}} service
{: #iam_grant}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and consistently control access to all cloud resources in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Complete the following steps to grant a user or service ID permissions to work with the {{site.data.keyword.sysdigsecure_full_notm}} service:

## Prerequisites
{: #iam_grant_sprereq}

Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.sysdigsecure_full_notm}} service. The account owner can grant user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/account?topic=account-userroles).


## Step 1. Create an access group
{: #iam_grant_step1}

Complete the following steps to create an access group:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Click **Create**.
3. Enter a name and optional description for your group, and click **Create**.

You can delete a group by selecting the **Remove group** option. When you remove a group from the account, you are removing all users and service IDs from the group and all access that is assigned to the group.
{: note}

To create an access group by using the CLI, you can use the [ibmcloud iam access-group-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_create) command.

```text
ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```
{: pre}



## Step 2. Add a policy
{: #iam_grant_step2}

After you set up your group, you can assign a common access policy to the group. You must add permissions to view {{site.data.keyword.sysdigsecure_full_notm}} instances in the Observability UI, to manage the instance in the {{site.data.keyword.cloud_notm}}, or both.

Any policy that you set for an access group applies to all entities, users, and service IDs, within the group.
{: note}

You can assign the policy by using the UI or through the command line.

When you define the policy, select a platform role and a service role.
- Platform management roles cover a range of actions, including the ability to create and delete instances, manage aliases, bindings, and credentials, and manage access. Valid platform roles are administrator, editor, operator, and viewer.
- Service access roles define a user's or service's ability to perform actions on a service instance. The service access roles are manager, writer, and reader.



### Add permissions through the CLI
{: #iam_grant_step2_1}

To create an access group policy by using the CLI, you can use the [ibmcloud iam access-group-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command.

```text
ibmcloud iam access-group-policy-create GROUP_NAME {-f, --file @JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```
{: codeblock}

Valid platform roles are `Administrator`, `Editor`, `Operator`, and `Viewer`.

Valid service roles are `Reader`, `Writer`, and `Manager`.

For example, you can run the following command to grant a user viewer permissions:

```text
ibmcloud iam access-group-policy-create my-access-group --roles Reader,Viewer --service-name my-monitoring-instance --service-instance 99999999-9999-9999-999999
```
{: pre}


### Add permissions through the UI
{: #iam_grant_step2_2}

Complete the following steps to assign a policy to an access group through the UI:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click **Access**  &gt; **Assign access** to create a policy.
4. In the **Service** section, select **{{site.data.keyword.sysdigsecure_full_notm}}**. Then, click **Next**.
5. In the **Resources** section, choose one of the following options:

    Select **All resources** to define the scope of the policy to include all instances.

    Select **Specific resources** to refine the scope of the policy. Then, configure 1 or more attributes: region, resource group, and service instance. Do not specify a value in the *Sysdig Team* section.

    Then, click **Next**.

6. Choose roles and actions to define the levels of access do you want to assign. You must choose a platform role and a service role.

    Add permissions to view {{site.data.keyword.sysdigsecure_full_notm}} instances in the Observability UI. Select a platform role such as **administrator** to grant admin permissions for the service. Select **viewer** to grant permissions to view instances in the *Observability* UI.

    [Learn more about the roles that you need](/docs/workload-protection?topic=workload-protection-iam).

7. Click **Review** &gt; **Add** &gt; **Assign**.





## Step 3. Add a user or service ID to the access group
{: #iam_grant_step3}

You can add users or service IDs to an existing group.

### Add a user to the access group
{: #iam_grant_step3_user}

Complete the following steps to add a user:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click **Add users** on the **Users** tab.
4. Select the users that you want to add from the list, and click **Add to group**.


### Add a service ID to the access group
{: #iam_grant_step3_svcid}

Complete the following steps to add a service ID:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the group that you want to assign access to.
3. Click the **Service IDs** tab, and click **Add service ID**.
4. Select the IDs that you want to add from the list, and click **Add to group**.
