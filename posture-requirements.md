---

copyright:
  years:  2023
lastupdated: "2023-05-16"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing requirements and requirement groups
{: #posture-requirements}

When you work with the {{site.data.keyword.sysdigsecure_full}} service, requirements and requirement groups can be created, edited, and removed in a custom policy.
{: shortdesc}

Requirements and requirement groups are not shared between policies.
{: important}

To reuse a requirement from another policy, you must create a new requirement group and requirement, and then link the wanted controls.

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy that you want to update.

2. Click **New Group**.

3. Enter the requirement group name and description.

4. Click **Save**. The new group is displayed.

5. You can optionally create subgroups.

   1. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the requirements group where you want to create a subgroup.

   2. Click **New Subgroup**.

   3. Enter the subgroup name and description.

   4. Click **Save**.

6. Add a requirement.

   1. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the requirements group or requirements subgroup where you want to add a requirement.

   2. Click **New Requirement**.

   3. Enter the requirement name and description.

   4. Click **Save**.

## Linking and unlinking controls
{: #control-links}

After you define your requirement groups and requirements, link controls to the policy.

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy to update.

2. Click the requirement within a requirements group in your policy.

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



## Deleting requirements
{: #reqmt-delete}

You can delete a requirement group or individual requirement. When you delete a group or requirement, all linked controls are deleted from the policy as well.

You can delete requirements and requirement groups only from custom policies.
{: note}

To delete requirements:

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy that you want to update.

2. Select a requirement group, subgroup, or individual requirement.

3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the selection to delete.

4. Click **Delete**.

5. Confirm you want to delete the item.
