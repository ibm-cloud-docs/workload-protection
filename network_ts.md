---

copyright:
  years:  2023
lastupdated: "2023-05-10"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Common networking configuration issues
{: #network_ts}

{{site.data.keyword.sysdigsecure_full}} provides a configuration page for administrators to fine-tune the way that the agent processes network data. The following are common configuration messages and how you can resolve the issues.
{: shortdesc}

## Namespaces without labels
{: #nw_nolabel}

Namespaces must be labeled for Kubernetes Network Policies (KNPs) to define ingress and egress rules.

If a namespace is not labeled, an error is displayed in the [network security policy tool.](/docs/workload-protection?topic=workload-protection-netsec_policy)

For example, if the Kube-system namespace is missing labels, you get the following error message:

```text
All communications are displayed as allowed because a policy can't be generated: you need to assign labels to this namespace.: kube-system
```
{: codeblock}

To resolve this issue, assign a label to the namespace. It will take a few minutes for the change to be detected by {{site.data.keyword.sysdigsecure_full_notm}}.



<!-- NEED TO ADD A SAMPLE , like kube-system -->





## Cluster subnet is incomplete
{: #nw_subnet}

To categorize unresolved IP addresses as being inside of outside a cluster, the agent needs to know the CIDR block ranges belonging to the cluster. By default the agent looks at the `kube-apiserver` and `kube-controller-manager` processes.

If the cluster subnets cannot be discovered automatically, a message that the cluster subnet is incomplete is displayed in the [network security policy tool.](/docs/workload-protection?topic=workload-protection-netsec_policy)

To resolve this issue, [configure CIDR block entries for your environment.](/docs/workload-protection?topic=workload-protection-network_config_ts#nw_cidr)

If configuring CIDR block entries for your environment doesn't resolve the issue, you might need to configure the agent to look for CIDR block ranges in other processes. Add the following to your agent `configmap` file:

```text
network_topology:
  pod_prefix_for_cidr_retrieval:
[<PROCESS_NAME>, <PROCESS_NAME>]
```
{: codeblock}

Where `PROCESS_NAME` is the name of the process to be searched.
