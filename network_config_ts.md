---

copyright:
  years:  2023
lastupdated: "2023-05-10"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Configuring your account
{: #network_config_ts}

{{site.data.keyword.sysdigsecure_full}} provides a configuration page for administrators to fine-tune the way that the agent processes network data.
{: shortdesc}

## Accessing the configuration page
{: #nw_launch}

To access the configuration page, do the following:

1. Open the [{{site.data.keyword.sysdigsecure_short}} UI](/docs/workload-protection?topic=workload-protection-launch).

2. Click the Network icon ![Network icon](/images/network.png "Network").

3. Click **Configuration**.

## Configuring workload labels
{: #nw_label}

{{site.data.keyword.sysdigsecure_full_notm}} automatically detects labels used for the Kubernetes objects in a cluster.

You might find there are many more labels than needed for network security purposes. You can use the **Workload Labels** to configure the default behavior for labels and whether to include or exclude specific labels for individual clusters. Excluded labels will not be displayed in the UI or included in network policies.

You can add multiple conditions selecting clusters, namespace labels, and workload labels as required.

Conditions you no longer need can be deleted with the exception of the `Default` condition. You must have a `Default` condition defined.

## Configuring actions for unresolved IPs
{: #nw_ips}

If the agent cannot resolve an IP address to a structure (for example, `Service`, `Deployment`, `Daemonset`, and so on), the IP address will be flagged as "unresolved" in the [**Ingress** and **Egress** views](/docs/workload-protection?topic=workload-protection-netsec_policy#knp_coms). In addition to resolving these IP addresses in the **Ingress** and **Egress** views you can add unresolved IP addresses or CIDR blocks in the **Unresolved IP Configuration** section of the **Configuration** page.

IP addresses and CIDR blocks can be associated with an alias and, optionally, set to "allowed" which will allow them to be included in a policy without being remediated each time they are encountered.

Grouping IP addresses with a single alias will not reduce entities in the [**Topology** map.](/docs/workload-protection?topic=workload-protection-netsec_policy#knp_map)
{: note}

## Configuring cluster CIDR blocks
{: #nw_cidr}

Unresolved IP addresses are flagged as `Internal` if they are inside the cluster or `External` if they are outside the cluster. `Unknown` IP addresses are those where subnet information is incomplete.

To resolve these situations one time for your environment, you can specify cluster and CIDR blocks for clusters in the **Cluster CIDR configuration**.

You can define `Default` internal CIDR blocks as well as CIDR blocks for individual clusters. Configurations that are no longer needed can be deleted.
