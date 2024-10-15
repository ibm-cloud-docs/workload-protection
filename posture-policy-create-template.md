---

copyright:
  years:  2023
lastupdated: "2023-05-16"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Creating a custom policy from a template
{: #posture-policy-create-template}

You can create custom policies in {{site.data.keyword.sysdigsecure_full}}.
{: shortdesc}


Complete the following steps to create a new policy with no prior policy as a base:

## Before you begin
{: #posture-policy-create-template-prereqs}

- In a policy, you can configure requirement groups to define the hierarchy and structure of controls in a policy.

    You can define 1 or more requirement groups per policy.

    Requirement groups are not shared between policies.

- In a requirement group, you can define 1 or more requirements. A requirement includes 1 or more controls.

    Requirements are not shared between policies.

    To reuse a requirement from another policy, you must create a new requirement group and requirement, and then link the wanted controls.


## Step 1. Create a policy
{: #posture-policy-create-template-step1}

Complete the following steps to create a policy that uses an existing policy as a template::

1. Create a policy draft by duplicating an existing policy in one of the following ways:

   * Click **New Policy** and for **Duplicate from** select the policy to be duplicated from the menu.

   * Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the policy that you want to use as a template and click **Duplicate**.

2. Enter a **Name** and **Desription** for the policy.

3. Click **Save**.

   Your policy is saved in a `Draft` state and you can configure the policy details.

If you create a new policy by duplicating an existing policy, the new policy is displayed with the requirements and controls that are copied from the duplicated policy. If you create a policy without duplicating an existing policy, the requirements and controls are blank.

![Example duplicated policy](images/duplicated-policy.png "An example of a duplicated policy"){: caption="An example of a duplicated policy" caption-side="bottom"}



## Step 2. Add requirement groups
{: #posture-policy-create-step2}

Complete the following steps to create a requirement group:

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy that you want to update.

2. Click **New Group**.

3. Enter the requirement group name and description.

4. Click **Save**. The new group is displayed.

5. You can optionally create subgroups.

   1. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the requirement group where you want to create a subgroup.

   2. Click **New Subgroup**.

   3. Enter the subgroup name and description.

   4. Click **Save**.




## Step 3. Add a requirement
{: #posture-policy-create-template-step3}

Complete the following steps to add a requirement:

1. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the requirement group or requirements subgroup where you want to add a requirement.

2. Click **New Requirement**.

3. Enter the requirement name and description.

4. Click **Save**.


## Step 4. Link controls to a requirement
{: #posture-policy-create-template-step4}

Complete the following steps to link controls to a requirement:

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy to update.

2. Click the requirement within a requirement group in your policy.

3. Click **Link Controls**. All available controls are displayed with the top-20 listed first.

   You can filter the list by:

   Severity
   :   The severity that is assigned to the control: high (H), medium (M), or low (L).

   Type
   :   The infrastructure type. For example, cluster, host, identity, or resource.

   Target
   :   The specfic platforms or distributions that a control evaluates resources against.

   You can also search on any word, or part of a word, in the control name.

   Multiple filters can be specified to create more specific filter expressions.
   {: tip}

4. Click **Link** for the control to link to the policy.

5. Repeat these steps to link more controls as needed.

If you need to unlink a control, hover over the linked control and click **Unlink**.
{: tip}


## Step 5. Publish the policy
{: #posture-policy-create-template-step5}


After configuring your policy, you need to publish the policy so that it is used in compliance evaluations.

These steps are only available for policies in draft state. The publish option is not available for policies that are already published.
{: note}

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy that you want to publish.

2. Click **Publish** and confirm that you want your policy published.

The date published is the date that the policy is activated.

If you change a published policy, the policy is reevaluated in the environment, and new results are displayed in the [**Compliance** view](/docs/workload-protection?topic=workload-protection-compliance). It can take a few minutes for the reevaluation to run and results to be refreshed.
