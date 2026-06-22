---

copyright:
  years:  2025, 2026
lastupdated: "2026-06-22"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Pricing
{: #pricing}

{{site.data.keyword.sysdigsecure_short}} offers two pricing plan options: free trial and graduated tier.
{: shortdesc}

The following table explains the differences between the free trial and the graudated tier pricing plan.

| Pricing plan  |  Description |
|---|---|
|  Free trial | The free trial plan enables you to try  all of the {{site.data.keyword.sysdigsecure_short}} capabilities available under the paid Graduated Tier plan. However, the Free Trial plan expires after 30 days, after which you have the option to upgrade to the Graduated Tier plan.  |
|  Graduated tier |   The graduated tier plan for {{site.data.keyword.sysdigsecure_short}} offers unified security and continuous compliance options for hosts, virtual machines, containers, OpenShift and Kubernetes, and multicloud environments.|
{: caption="Pricing plans for {{site.data.keyword.sysdigsecure_short}}." caption-side="bottom"}

## How pricing units are calculated
{: #pricing_pricing-units}

All pricing units are calculated based on monthly or hourly cost and prorated based on consumption usage. For more information about pricing, check out [how you're charged](/docs/account?topic=account-charges).

| Use case  | Pricing unit  |  Environment or workload  |  Billable resources |
|---|---|---|---|
| CSPM (agentless)  | Multicloud CSPM compute instances | Cloud environments, including multicloud | {{site.data.keyword.cloud_notm}} VSIs, IBM PowerVS Instances, Worker Nodes, Baremetal servers for VPC, AWS EC2, Azure VMs, GCP Compute Instances, Oracle OCI Compute Instances. |
| Kubernetes protection (agent-based) | Node hours (worker) | Containerized on cloud or on-premises, including Kubernetes/OpenShift | Worker nodes on IKS/ROKS, AKS/ARO, GKE, OKE |
| Host protection (agent-based) | VM node hours | Virtualized on cloud or on-premises, including VMs | Including VMs such as Linux Hosts, Windows OS, AIX, VMware, Power, PowerVS, Open Stack, or other private clouds. |
{: caption="The different ways you're charged depending on the use case." caption-side="bottom"}

{{site.data.keyword.sysdigsecure_short}} performs scans for all connected {{site.data.keyword.cloud_notm}} accounts every 24 hours. The 24-hour schedule begins as soon as you connect an account for the first time. On-demand scanning is also supported at no additional charge.
{: tip}

## How the graduated tier plan works
{: #pricing_plan-works}

The graduated tier plan is the paid plan for {{site.data.keyword.sysdigsecure_short}}. Tiers are measured by the number of pricing units they contain. Pricing units are segmented into three categories: CSPM usage, active {{site.data.keyword.sysdigsecure_short}} agents, and deployment environments for {{site.data.keyword.sysdigsecure_short}} agents. The graduated tier plan offers discounts as you increase the number of pricing units, allowing you to stack pricing unit tiers as your coverage needs increase. Discounts are applied as you move from one tier to the next.

If you are using {{site.data.keyword.sysdigsecure_short}} for CSPM, you are charged the list price for tier one (up to 250 pricing units). The discount for tier two starts at unit 251 and continues to unit 500, with the next tier starting at unit 501, and so on.

Container and host protection with agents is charged hourly. The list price applies for tier one (up to 180,000 node hours). The discount for tier two starts at hour 180,001 and continues to hour 360,000, with the next tier starting at hour 360,001, and so on.

For more detailed pricing information, check out [{{site.data.keyword.sysdigsecure_short}} in the catalog](https://cloud.ibm.com/workload-protection/catalog/security-and-compliance-center-workload-protection).

If you are using both {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.mon_short}}, it’s important to remember that you do not need to deploy an individual agent for each on the same cluster. A single agent works for both products. You should connect your {{site.data.keyword.mon_short}} and {{site.data.keyword.sysdigsecure_short}} instances during the instance creation. For more information, check out the [frequently asked questions](/docs/monitoring?topic=monitoring-faq#faq_4).
{:note}
