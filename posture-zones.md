---

copyright:
  years:  2023
lastupdated: "2023-05-16"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing zones
{: #posture-zones}

In {{site.data.keyword.sysdigsecure_full}}, a zone is a collection of scopes that represent important areas of your business. For example, a zone might be your production environment or staging environment. You can also define zones as various regions.
{: shortdesc}

Two zones are provided by default:

`Entire infrastructure`
:   This zone includes all connected data sources. CIS policies and {{site.data.keyword.sysdigsecure_short}} Kubernetes policies are automatically applied to this zone. Findings are reported on the [**Compliance** page.](/docs/workload-protection?topic=workload-protection-compliance)

    To apply other policies, apply them to individual zones.

`Entire Git`
:   If you configured integrations with your Git repositories, then `Entire Git` zone includes those source repositories.

You can create targeted zones for specific data sources or Git repositories as needed.

## Creating and configuring zones
{: #posture-zones-create-zone}

A zone is consisted of:

* The name of the zone.
* The description of the zone.
* The scope of the zone.
* Any applied policies.

To configure a zone, do the following steps:

1. Open the [{{site.data.keyword.sysdigsecure_short}} UI](/docs/workload-protection?topic=workload-protection-launch).

2. Hover over the **Inventory** and click **Zones** in the *Posture* section.

3. Click **New Zone**.

4. Enter a **Name** and **Description** for your zone and click **Create**.

   If necessary, you can update the **Name** and **Description** on the next page.
   {: tip}

5. Click **Add Scope** and select the scope rules for each platform.

   Scope rules for supported platforms are:

   Kubernetes
   :    Distribution (AKS, GKE, EKS, default Kubernetes), cluster name, namespace, and labels

   Host
   :    Cluster

   Git
   :    Git integration and Git sources

   AWS
   :    Organization, account, region, labels

   Azure
   :    Organization, subscription, region, labels

   GCP
   :    Organization, project, region, labels, host (for Docker, Linux hosts), and cluster

6. Click **Save**.

The created zone is displayed on the **Zones** page.

If you created a zone where no relevant resources are available for the selected policies, no results are displayed on the [**Compliance** page.](/docs/workload-protection?topic=workload-protection-compliance)


## Applying policies to a zone
{: #posture-zones-policy-apply}

To apply policies to a zone, complete the following steps:

1. Open the [{{site.data.keyword.sysdigsecure_short}} UI](/docs/workload-protection?topic=workload-protection-launch).

2. Hover over the **Policies** icon ![Policies icon](/images/policies.png "Policies") and click **Policies** in the *Posture* section.

3. Select the Policy you want to assign and click on the three dots on the right and *Assign Zones*.

4. Under *Assigned Zones* select the Zone(s) you want to assign.

5. Click **Save**.

When you apply a policy in a zone that does not have in scope resources relevant to that policy, results will not appear on the Compliance page.
{: note}

## Removing policies from a zone
{: #posture-zones-policy-remove}

To remove policies to a zone, complete the following steps:

1. Open the [{{site.data.keyword.sysdigsecure_short}} UI](/docs/workload-protection?topic=workload-protection-launch).

2. Hover over the **Policies** icon ![Policies icon](/images/policies.png "Policies") and click **Policies** in the *Posture* section.

3. Select the Policy you want to assign and click on the three dots on the right and *Assign Zones*.

4. Under *Assigned Zones* remove the Zone(s) you want to assign.

5. Click **Save**.

## Modifying a zone
{: #posture-zones-modify-zone}

To modify a custom zone's configuration, do the following steps:

1. Open the [{{site.data.keyword.sysdigsecure_short}} UI](/docs/workload-protection?topic=workload-protection-launch).

2. Hover over the **Inventory** and click **Zones** in the *Posture* section.

3. Click the zone that you want to modify.

4. Make your required changes.

5. Click **Save**.

## Deleting zones
{: #posture-zones-delete-zone}

You can delete a zone that you no longer need.

1. Open the [{{site.data.keyword.sysdigsecure_short}} UI](/docs/workload-protection?topic=workload-protection-launch).

2. Hover over the **Inventory** and click **Zones** in the *Posture* section.

3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") next to the zone that you want to delete.

4. Click **Delete**.

5. Click **Yes, Delete** to confirm you want to delete the zone.
