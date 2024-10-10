---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords: IBM Cloud, monitoring, overview, personal data, data deletion, PHI, data, data security, _service-name_

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Managing data
{: #data-security}

To ensure that you can securely manage your data when you use{{site.data.keyword.sysdigsecure_full_notm}}, it is important to know exactly what data is stored and encrypted, and how you can delete any stored personal data.
{: shortdesc}


## How your data is collected in {{site.data.keyword.sysdigsecure_full_notm}}
{: #data-collection}

When you configure an agent to collect and forward data to an {{site.data.keyword.sysdigsecure_full_notm}} instance, data is automatically collected and available for analysis through the web UI. You can configure the agent to connect to the instance via the public network or the private network.

To connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network, you can configure an agent to send data by using a public endpoint. The environment where the agent is running requires internet access to use the public endpoint.

You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. To configure an agent to send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account. Once the account is VRF enabled, the agent can be configured to use the private network by using the [Private Endpoint](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion) as the ingestion URL.
* Private endpoints are not accessible from the public internet.
* All traffic is routed to the {{site.data.keyword.cloud_notm}} private network.


## How your data is stored in {{site.data.keyword.sysdigsecure_full_notm}}
{: #data-storage}

{{site.data.keyword.sysdigsecure_full_notm}} collects and aggregates data.

### Data location
{: #data_storage_location}

Metric data is hosted on the {{site.data.keyword.cloud_notm}}.
* Each multi-zone region (MZR) location collects and aggregates metrics for each instance of the {{site.data.keyword.sysdigsecure_full_notm}} that runs in that location.
* Data is colocated in the region where the {{site.data.keyword.sysdigsecure_full_notm}} instance is provisioned. For example, data for an instance that is provisioned in US South is hosted in the US South region.


### Data retention
{: #data_storage_retention}

Data is retained as follows, including when an agent is uninstalled, and the host or instance is no longer monitored.

| Data type | Retention |
| -------------- | -------------- |
| policy events `[*]` | 1M events or 90 days |
| activity audit `[*]` | 90 days |
| benchmarks `[*]` | 90 days |
| scan results `[*]` | Image data is kept for a maximum of 90 days. \n  \n A maximum of 5 tags for each  repository and a maximum of 5 different images for each tag are retained. If an additional image is pushed when 5 images exist, the oldest image will be deleted, regardless of age.  \n  \n Images used by a container monitored by a {{site.data.keyword.sysdigsecure_full_notm}} agent (runtime images) are always retained regardless of limits. |
| vulnerability management reports | 15 days|
| captures | 90 days |
{: caption="Data retention" caption-side="bottom"}

`[*]` - Conditions are applied simultaneously.  The retention policy will be triggered for the first matched retention trigger.

Data is available for analysis through the web UI for the time period that the agent was installed and reporting.

After you delete an instance of the {{site.data.keyword.sysdigsecure_full_notm}} service, data is not available for search and analysis.

## Deleting your data
{: #data-delete}

### Deleting user metadata
{: #service-delete-metadata}

User metadata, such as rules, policies, teams, and users, is never deleted.

You must open a case through support to request the metadata to be deleted. For more information, see [Open a support ticket](/docs/get-support?topic=get-support-open-case).


### Deleting a subset of data
{: #service-delete-agent}

Deletion of a subset of data is not supported.

For example, deletion of data that is collected from 1 agent in a {{site.data.keyword.sysdigsecure_full_notm}} instance is not supported.



### Deleting an {{site.data.keyword.sysdigsecure_full_notm}} instance
{: #service-delete}

When you delete an instance of {{site.data.keyword.sysdigsecure_full_notm}} from the {{site.data.keyword.cloud_notm}}, you must open a case through support to request the data to be deleted. For more information, see [contacting support](/docs/workload-protection?topic=workload-protection-gettinghelp#gettinghelp).
