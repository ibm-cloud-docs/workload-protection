---

copyright:
  years:  2023
lastupdated: "2023-09-18"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Pricing for for IBM Cloud Security and Compliance Center Workload Protection
{: #pricing_plans}

Pricing for {{site.data.keyword.sysdigsecure_full_notm}} is based on a graduated tier system in which costs decrease per-resource as you deploy more resources. Your cost depends on how many {{site.data.keyword.sysdigsecure_short}} agents that you have and where those agents are deployed.
{: shortdesc}

For an up-to-the-minute look at the metrics and tiers used to determine costs, check out the [catalog page for {{site.data.keyword.sysdigsecure_short}}](https://cloud.ibm.com/catalog/services/security-and-compliance-center-workload-protection).
{: tip}

A free trial of {{site.data.keyword.sysdigsecure_short}} is available for users who want to try the service out. It includes all of the capabilities of the paid plan and expires after 30 days unless you upgrade it to a paid plan.

## How pricing works in Workload Protection
{: #pricing_plans-works}

Your monthly charge is pro-rated based on the amount of time within that month you have had a resource deployed. You are not charged for time during a month when a resource was not deployed.
{: tip}

There are two usage metrics used to determine pricing. Both are calculated **per month**:

1. **Node hours**: this metric is used for agents deployed on nodes in Kubernetes clusters inside IBM Cloud (typically, one agent is deployed per node). Although the metric is calculated per hour, bills are issued monthly, so it is helpful to remember that a month with 30 days has 720 hours.
2. **Multi-cloud cloud security posture management (CSPM) compute instances**: this metric is used for agents deployed on clouds other than {{site.data.keyword.cloud_notm}} and is calculated per month.

Both pricing plans use a **graduated tiered** system, in which you are charged based on the number of resources that are deployed. For example, if the first tier is 10 cents for the first 250 resources, and five cents for the next 250 resources, and you have 300 resources, you would pay USD 27.50 per month; USD 25 for the resources in the first tier, and USD 2.50 for the resources in the next tier. For more information about pricing, check out [How you're charged](/docs/billing-usage?topic=billing-usage-charges).

The {{site.data.keyword.sysdigsecure_short}} agent and the {{site.data.keyword.mon_short}} agent cannot be deployed on the same cluster. However, you can access {{site.data.keyword.sysdigsecure_short}} functionality through {{site.data.keyword.mon_short}} by selecting the **Graduated Tier - Sysdig Secure + Monitor** plan. For more information, check out [Service plans](/docs/monitoring?topic=monitoring-service_plans).
{: note}
