---

copyright:
  years: 2026
lastupdated: "2026-06-16"

keywords: vulnerabilities, agent, security scanning

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Completing agent setup
{: #vulnerabilities-next}

Configure security policies, verify agent installation, and schedule reports after you add the {{site.data.keyword.sysdigsecure_short}} agent to your environment.
{: shortdesc}

## Verifying agent installation
{: #verify}

After you add an agent, verify that it was deployed correctly.

1. Go to the [{{site.data.keyword.cloud_notm}} Compliance](/security/compliance) page.
2. Select your {{site.data.keyword.sysdigsecure_short}} instance.
3. Click **Open dashboard**.
4. Click **Inventory** to confirm that your resources appear in the list.
5. Then, go to **Integrations > Environments > Sysdig Agents** and confirm that your agent appears in the list.

If you [added an agent to an AIX host](/docs/workload-protection?topic=workload-protection-agent-deploy-aix-powervs), you can view the agent only on the **Inventory** page. The agent does not appear on the **Sysdig Agents** page.
{: important}

## Reviewing results 
{: #review-results}

After you verify your agent was successfully installed, you can view compliance results, vulnerability scan results, and threat detections. It might take up to 24 hours for the first scans to complete. 

1. Go to the [{{site.data.keyword.cloud_notm}} Compliance](/security/compliance) page.
2. Select your {{site.data.keyword.sysdigsecure_short}} instance.
3. Click **Open dashboard**.
4. To view compliance scan results, go to **Attack Surface > Compliance Findings**. 
5. To view vulnerability scan results, go to **Dashboards > Vulnerabilities**.
6. To view threat detections, go to **Detection & Response > Threats**. 

## Setting up security policies
{: #vulnerabilities-next-policies}

{{site.data.keyword.sysdigsecure_short}} provides default security policies for your environment. You can customize these policies to meet your specific security requirements. For more information, see [Securing containers and hosts with agents](/docs/workload-protection?topic=workload-protection-about#use-cases-agents).

## Configuring agent settings
{: #fine-tune}

You can customize how the agent processes network data.

1. From your {{site.data.keyword.sysdigsecure_short}} instance, click **Open dashboard**.
2. Go to **Inventory > Network**.
3. Select your cluster and namespace.
4. Click **Configuration**.

### Configuring workload labels
{: #nw_label}

{{site.data.keyword.sysdigsecure_full_notm}} automatically detects labels that are used for Kubernetes objects in a cluster.

You might find that there are more labels than needed for network security purposes. You can use **Workload Labels** to configure the default behavior for labels and to include or exclude specific labels for individual clusters. Excluded labels are not displayed in the UI or included in network policies.

You can add multiple conditions by selecting clusters, namespace labels, and workload labels as required.

You can delete conditions that you no longer need, except for the `Default` condition. You must have a `Default` condition defined.

### Configuring actions for unresolved IP addresses
{: #nw_ips}

If the agent cannot resolve an IP address to a structure (for example, `Service`, `Deployment`, or `Daemonset`), the IP address is flagged as `unresolved` in the **Ingress** and **Egress** views. In addition to resolving these IP addresses in the **Ingress** and **Egress** views, you can add unresolved IP addresses or CIDR blocks in the **Unresolved IP Configuration** section of the **Configuration** page.

You can associate IP addresses and CIDR blocks with an alias and, optionally, set them to `allowed`, which allows them to be included in a policy without being remediated each time they are encountered.

Grouping IP addresses with a single alias does not reduce entities in the topology map.
{: note}

### Configuring cluster CIDR blocks
{: #nw_cidr}

Unresolved IP addresses are flagged as `Internal` if they are inside the cluster or `External` if they are outside the cluster. `Unknown` IP addresses are those where subnet information is incomplete.

To resolve these situations for your environment, you can specify cluster and CIDR blocks for clusters in the **Cluster CIDR configuration** section.

You can define `Default` internal CIDR blocks and CIDR blocks for individual clusters. You can delete configurations that are no longer needed.
