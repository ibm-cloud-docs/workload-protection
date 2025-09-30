---

copyright:
  years:  2025
lastupdated: "2025-06-26"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Pricing 
{: #pricing}

{{site.data.keyword.sysdigsecure_short}} offers two pricing plan options: Free Trial and Graduated Tier. Reference the table below for more information about these plans. 
{: shortdesc}

|   |   |
|---|---|
|  Free Trial | The Free Trial plan enables you to try  all of the {{site.data.keyword.sysdigsecure_short}} capabilities available under the paid Graduated Tier plan. However, the Free Trial plan expires after 30 days, after which you have the option to upgrade to the Graduated Tier plan.  |
|  Graduated Tier |   The Graduated Tier plan for {{site.data.keyword.sysdigsecure_short}} offers unified security and continuous compliance options for hosts, virtual machines, containers, OpenShift and Kubernetes, and multicloud environments.|
{: caption="The two different plans." caption-side="bottom"}

## How Pricing Units are calculated
{: #pricing_pricing-units}

All pricing units are calculated based on monthly or hourly cost and prorated based on consumption usage. For more information about pricing, check out [how you're charged](/docs/account?topic=account-charges). 

| Use Case  | Pricing Unit  |  Environment / Workload  |  Supported |
|---|---|---|---|
| CSPM (agentless)  | Multicloud CSPM Compute Instances | Cloud environments, including multicloud | {{site.data.keyword.cloud_notm}} VSIs, IBM PowerVS Instances, Worker Nodes, Baremetal servers for VPC, AWS EC2, Azure VMs, GCP Compute Instances, Oracle OCI Compute Instances. |
| Kubernetes Protection (agent-based) | Node Hours (Worker) | Containerized on Cloud or on-premises, including Kubernetes/OpenShift | Worker nodes on IKS/ROKS, AKS/ARO, GKE, OKE |
| Host Protection (agent-based) | VM Node Hours | Virtualized on Cloud or on-premises, including VMs | Including VMs such as Linux Hosts, Windows OS, AIX, VMware, Power, PowerVS, Open Stack, or other private clouds. |
{: caption="The different ways you're charged depending on the use case." caption-side="bottom"}

{{site.data.keyword.sysdigsecure_short}} performs scans for all connected {{site.data.keyword.cloud_notm}} accounts every 24 hours. The 24-hour schedule begins as soon as you connect an account for the first time. On-demand scanning is also supported at no additional charge.
{: tip}

## How Graduated Tiers Work 
{: #pricing_plan-works}

The **Graduated Tier plan** is the paid plan for {{site.data.keyword.sysdigsecure_short}}. Tiers are measured by the number of pricing units they contain. Pricing units are segmented into three categories: CSPM usage, active {{site.data.keyword.sysdigsecure_short}} agents, and deployment environments for {{site.data.keyword.sysdigsecure_short}} agents.

The Graduated Tier plan offers discounts as you increase the number of pricing units, allowing you to stack pricing unit tiers as your coverage needs increase. Discounts are applied as you move from one tier to the next. Using the chart below as an example, you are charged list price for tier 1 (up to 250 pricing units). The discount for tier 2 starts at unit 251 and continues to unit 500, with the next tier starting at unit 501, and so on. 

| Pricing Unit Tiers  | Compute Instance  |  Worker Nodes  |  VM Nodes |
|---|---|---|---|
| 1–250   | $18 | $45 | $16 |
| 251–500   | $15.30 | $38.25 | $13.60  |
| 501–1,000   | $13.50 | $33.75 | $12 |
| 1,001–2,500   | $12.60 | $31.50 | $11.20  |
| 2,501–5,000   | $10.80 | $27 | $9.60  |
| 5,001   | $9.90 | $24.75 | $8.80  |
{: caption="The above prices are estimates. Pricing is subject to change and does not reflect pricing differences by region. Tiers are based on the volume of pricing units. " caption-side="bottom"}

To start pricing for {{site.data.keyword.sysdigsecure_short}}, check out the [{{site.data.keyword.sysdigsecure_short}} catalog](https://cloud.ibm.com/workload-protection/catalog/security-and-compliance-center-workload-protection).  
{: tip}

If you are using both {{site.data.keyword.sysdigsecure_short}} and {{site.data.keyword.mon_short}}, it’s important to remember that you do not need to deploy an individual agent for each on the same cluster. A single agent works for both products. You should connect your {{site.data.keyword.mon_short}} and {{site.data.keyword.sysdigsecure_short}} instances during the instance creation. For more information, check out the [frequently asked questions](/docs/monitoring?topic=monitoring-faq#faq_4).
{:note}
