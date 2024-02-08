---

copyright:
  years:  2023
lastupdated: "2023-09-26"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing Posture Policies
{: #posture-policies}

You can use the {{site.data.keyword.sysdigsecure_full}} Posture Policies to manage policies in your environment.
{: shortdesc}

For more information about how an instance of {{site.data.keyword.sysdigsecure_full_notm}} can be integrated with {{site.data.keyword.compliance_short}} to run scans that validate your level of compliance, check out [Connecting Workload Protection](/docs/security-compliance?topic=security-compliance-setup-workload-protection).
{: tip}

A control describes a rule, the code that is run to evaluate it, and a remediation playbook to fix the violation that might be detected. There are different types of controls to address business, security, compliance, and operational requirements. For more information, see [Posture controls](/docs/workload-protection?topic=workload-protection-posture-controls).

A policy is a combination of rules about the activities that the enterprise wants to detect in an environment. These policies can be modified to meet specific needs. A policy includes one or more controls to define a compliance standard, a benchmark, or a business policy.

With **Postures Policies** you can:

* Clone an existing policy and edit its metadata.
* Create, edit, and delete custom policies.
* Create, edit, and delete requirements in a custom policy.
* Link and unlink controls to policy requirements.

One way of creating a new policy would be to:

1. Select an existing policy to use as a template.
2. Create or edit requirements that are associated with the policy.
3. Linking or unlinking controls.
4. Saving the policy with a new name.

You can also create policies without using an existing policy as a template.

Policies are not run in your environment until they are published. Keeping policies in a draft state give you the time to design and configure the policies that you need without affecting your running compliance scans.
{: tip}

## Accessing Posture Policies
{: #access-posture-controls}

To access the **Posture Policies**:

1. Open the [{{site.data.keyword.sysdigsecure_short}} UI](/docs/workload-protection?topic=workload-protection-launch).

2. Hover over the **Policies** icon ![Policies icon](/images/policies.png "Policies") and click **Policies** in the *Posture* section. The configured policies are displayed.

## Creating a custom policy
{: #create-policy}

You can create a custom policy by duplicating an existing policy or creating a new policy from the beginning. Choose one of the following options:

- [Creating a custom policy from scratch](/docs/workload-protection?topic=workload-protection-posture-policy-create).
- [Creating a custom policy from a template](/docs/workload-protection?topic=workload-protection-posture-policy-create-template).



## Deleting policies
{: #policy-delete}

Deleting an active policy deletes the policy and policy's evaluation history.

You can delete only custom policies.
{: note}

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy that you want to delete.

2. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the selection to delete.

3. Click **Delete**.

4. Confirm you want to delete the policy.


## Editing policies
{: #policy-edit}

You can edit custom policies. Default policies cannot be edited.

You can change:

* The policy name and description
* The requirement groups and requirement names and descriptions
* The requirement groups and requirements. You can add or delete groups as required.
* Whether controls are linked or unlinked
* Whether a control is activated or deactivated

   Deactivated controls are associated with a requirement, but are not included when the evaluation is run.
   {: note}

To edit a policy:

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy that you want to update.

2. Make your changes.

3. When complete, [publish your changes.](#publish-policy)



## Publishing policies
{: #publish-policy}

After configuring your policy, you need to publish the policy so that it is used in compliance evaluations.

These steps are only available for policies in draft state. The publish option is not available for policies that are already published.
{: note}

1. Open your policy by [accessing the **Posture Policies** view](#access-posture-controls) and clicking the policy that you want to publish.

2. Click **Publish** and confirm that you want your policy published.

The date published is the date that the policy is activated.

If you change a published policy, the policy is reevaluated in the environment, and new results are displayed in the [**Compliance** view](/docs/workload-protection?topic=workload-protection-compliance). It can take a few minutes for the reevaluation to run and results to be refreshed.
