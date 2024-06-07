---

copyright:
  years:  2023
lastupdated: "2023-01-04"

keywords: IBM Cloud, Sysdig Secure, teams

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Working with teams
{: #teams}

You can use teams to add another dimension of control on the data that is available through an instance in addition to platform and service access controls.
{: shortdesc}

- A user with the **Editor** service role for an {{site.data.keyword.sysdigsecure_full_notm}} instance can create, delete, add members, and change the scope of teams in that instance. Once a team is created, an admin can add a user to it through {{site.data.keyword.iamlong}} (IAM).
- A user with the **Administrator** platform role for an instance can invite users to the account, and can create, delete, add members, and change the scope of teams in that instance. Once a team is created, an admin can add a user to it through {{site.data.keyword.iamlong}} (IAM).

By using teams, administrators can apply a fine grain control on resources. Consider the following information when you work with teams:
* You can create 1 or more teams in an instance.
* You can specify what resources and metrics are visible for users that are granted IAM permissions to work in the team.
* You can enhance the users experience by customizing the initial dashboard that users in a team get when they launch the web UI.
* Use a unique name for each team that you define in any instance of the {{site.data.keyword.sysdigsecure_full_notm}} service.
* If you use {{site.data.keyword.sysdigsecure_full_notm}} and {{site.data.keyword.mon_full_notm}}, make sure the names of the teams that you define in any of the instances of either product are unique.

    For example, if you define a team in {{site.data.keyword.sysdigsecure_full_notm}} with the same name as a team that is created in {{site.data.keyword.mon_full_notm}}, you will get an error and the team will not be created.

These instructions assume that you have provisioned a service instance on {{site.data.keyword.cloud_notm}}.
{: note}






## Assigning a user to a team by using access groups
{: #teams_assign_ag}

To add 1 or more users to a team by using access groups, you must define 2 policies on the {{site.data.keyword.sysdigsecure_full_notm}} service at the access group level. Any users that belong to that access group will inherit the permissions to work with that team.
- The first policy defines permissions on 1 instance or at the account level that specify the platform permissions to manage the service.
- The second policy defines the permissions to operate the service within the context of 1 team.


To add 1 or more users to a team, complete the following steps:
1. Check that you have the **administrator** platform role if you need to invite users to the account.
2. Check that you have the **administrator** platform role or the **editor** service role to work with the service or with a specific instance so that you can grant a user permissions and add a user to a team.
3. Define a policy to allow users to launch an instance or manage the service on {{site.data.keyword.cloud_notm}}.
4. Define a policy on a team. When this policy is defined, the user is added to the list of users that have access to work with resources configured for a team.

For more information, see [Granting permissions to work in a team](/docs/workload-protection?topic=workload-protection-iam_grant_team).


## Assigning a user to a team
{: #teams_assign_user}

To add a user to a team, you must define 2 policies on the {{site.data.keyword.sysdigsecure_full_notm}} service for the user:
- The first policy defines permissions on 1 instance or at the account level that specify the platform permissions to manage the service.
- The second policy defines the permissions to operate the service within the context of 1 team.

To add a user to a team, complete the following steps:
1. Check that you have the **administrator** platform role if you need to invite users to the account.
2. Check that you have the **administrator** platform role or the **editor** service role to work with the service or with a specific instance so that you can grant a user permissions and add a user to a team.
3. Define a policy to allow the user to launch an instance or manage the service on {{site.data.keyword.cloud_notm}}.
4. Define a policy on a team. When this policy is defined, the user is added to the list of users that have access to work with resources configured for a team.

For more information, see [Granting permissions to work in a team](/docs/workload-protection?topic=workload-protection-iam_grant_team).




## Creating a team
{: #teams_create}

You must have **manager** role to create a team in an instance.

An administrator or a manager of an {{site.data.keyword.sysdigsecure_full_notm}} instance must switch to the *Secure Operations* team before he can create teams and manage existing teams.
{: note}

Complete the following steps to create a team:

1. [Launch the web UI](/docs/workload-protection?topic=workload-protection-launch#launch).

2. Click the **user icon**.  This is the icon with the initials of the logged on user.  Then click **Settings**.

3. Click **Teams**. The list of existing teams is displayed.

4. Click **Add Team**. The team configuration page is displayed.

5. Configure the team details.

    * Choose a color.

    * Enter the name of the team

    * [Optional] Enter a description for this team.

    * [Optional] Set the **Default team** parameter if you want this team to become the default team for new users.

    * Set the **Default Entry Point** to specify the view in the web UI that opens every time a user logs in. By default, the *Explore* view is set.

6. Click **Save**.

![Team Configuration](images/team-configuration.png "Team Configuration"){: caption="Figure 1. Team configuration" caption-side="bottom"}


## Deleting a team
{: #teams_delete}

You must have **manager** role to delete a team in an instance.

Complete the following steps to delete a team:

The default team, **Secure Operations**, cannot be deleted.
{: note}

1. Launch the web UI. For more information on how to launch the Web UI, see [Navigating to the Web UI](/docs/workload-protection?topic=workload-protection-launch#launch).

2. Click the **user icon**.  This is the icon with the initials of the logged on user.  Then click **Settings**.

3. Select **Teams**. The list of existing teams is displayed.

4. Identify the team that you want to delete and select it. The details of the team are displayed.

5. Click **Delete team**.

When you delete a team, users that only belong to this team will be moved to the default team.
{: important}
