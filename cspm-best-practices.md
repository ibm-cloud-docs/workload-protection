---

copyright:
  years:  2024
lastupdated: "2024-07-08"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Best Practices for working with Workload Protection for {{site.data.keyword.cloud_notm}} CSPM
{: #cspm-best-practices}

{{site.data.keyword.sysdigsecure_full}} now supports Cloud Security Posture Management (CSPM) for {{site.data.keyword.cloud_notm}} resources with the {{site.data.keyword.cloud_notm}} Framework for Financial Services, Digital Operational Resilience Act (DORA), CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark, PCI, and many other industrial related or best practices standards.

## Managing posture policies
{: #cspm-best-practices-manage-policies}

In {{site.data.keyword.sysdigsecure_short}}, posture policies are collections of controls that you use to evaluate your compliance. You can use the predefined policies or create custom ones. 

### Predefined compliance policies
{: #cspm-best-practices-manage-policies-compliance}

Predefined policies are updated regularly with fixes, new parameters and checks, and with new versions of the compliance program. You have available many predefined policies such as {{site.data.keyword.cloud_notm}} resources with {{site.data.keyword.cloud_notm}} Framework for Financial Services, Digital Operational Resilience Act (DORA), CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark, or PCI.

When you start implementing CSPM for {{site.data.keyword.cloud_notm}}, your services will be evaluated against all available {{site.data.keyword.cloud_notm}} controls (All Posture Findings) and the CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark and you can apply other policies as described next.

### Applying posture policies
{: #cspm-best-practices-manage-policies-applying}

By default, {{site.data.keyword.sysdigsecure_short}} creates a scope for all of your connected {{site.data.keyword.cloud_notm}} services, clusters and workloads in a Zone called **Entire Infrastructure**. You can apply new posture policies to this zone or create a new zone to scope your resources.

To apply a policy to a zone go to **Policies / Zones** and link the policy to the zone:
- If the zone exists, add the policy by using the [Zones configuration page](/docs/workload-protection?topic=workload-protection-zone-policy).
- If the zone does not exist, [create and configure the zone](/docs/workload-protection?topic=workload-protection-posture-zones), and then add the policy by using the Zones configuration page.

### Creating custom posture policies
{: #cspm-best-practices-manage-policies-custom}

If you want to take control of the controls, requirements, or names of your posture policies, with {{site.data.keyword.sysdigsecure_short}}, you can create custom policies based on the existing or customized controls. 

- Learn how to to create your own policy from scratch [here](/docs/workload-protection?topic=workload-protection-posture-policy-create).
- Learn how to to create your own policy starting from an existing posture policy [here](/docs/workload-protection?topic=workload-protection-posture-policy-create-template).

## Reviewing posture results and downloading reports
{: #cspm-best-practices-review-reports}

When you start implementing CSPM for {{site.data.keyword.cloud_notm}}, your services will be evaluated against all available {{site.data.keyword.cloud_notm}} controls and the CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark and you can apply other policies as described in previous sections.

After the first completed scan (that can take some minutes after the integration) the Posture results will be shown under **Posture / Compliance**:

1. Select the policy you want to review.
2. Select the requirement(s) to analyze.
3. Click on **Show controls** and **show results**.
4. You will see listed all the affected resources by that particular control.
5. When clicking on **View Remediation** you will get the steps to remediate that control. 
6. In this same view, you can **Accept Risk** for removing the violation from the failed control for that resource. Select the risk reason and (optional) expiration to complete the accept risk creation.

From a particular policy results view, you can download a report by clicking on **Download Report** that will generate a CSV with all the results for the controls of the select policy.

## Reviewing all connected resources in Inventory
{: #cspm-best-practices-review-resources}

Once you have implemented CSPM for your {{site.data.keyword.cloud_notm}} account(s), all your {{site.data.keyword.cloud_notm}} resources (and any other connected data source such as Kubernetes/OpenShift resources or multi-cloud environments) will be listed under [**Inventory**](/docs/workload-protection?topic=workload-protection-inventory).

Use the **Feature Filters** to quickly filter by the most used filter types. It lets you narrow down to your most prevalent and at-risk resources, including resource counting and risk indicators.

For each resource, click on the resource card to access the **Posture** and **Configuration** tab:
- The **Posture** tab indicates the number of failed policies. Select a failed policy to see the relevant controls to be remediated. The controls are grouped by requirement within each policy.
- The **Configuration** tab contains additional metadata and configuration details including the timestamp when the resource was last scanned.

## Customizing controls
{: #cspm-best-practices-customize-controls}

{{site.data.keyword.sysdigsecure_short}} incrementally adds the ability to customize posture control by adding parameters defined within posture controls.

You can see all the available [Posture controls](/docs/workload-protection?topic=workload-protection-posture-controls) under Policies > Controls. Select the control you want to customize and select **Parameters**, then click on **Customize** and change the parameters based on your requirements.

In addition to modifying the parameters of existing controls, you can duplicate and edit any control as described [here](https://docs.sysdig.com/en/docs/sysdig-secure/policies/posture-policies/posture-controls/#custom-controls).

## Organize your accounts and resources
{: #cspm-best-practices-organize}

By default, {{site.data.keyword.sysdigsecure_short}} creates a scope for all your connected {{site.data.keyword.cloud_notm}} services, clusters and workloads in a zone called **Entire Infrastructure**. You can apply new posture policies to this zone or create a new zone to scope your resources.

You can [create your own scopes](https://cloud.ibm.com/docs/workload-protection?topic=workload-protection-posture-zones) based on region or account IDs. In the near future, also resource labels will be available for defining scope.

## Next steps
{: #cspm-best-practices-next-steps}

To get the most of {{site.data.keyword.sysdigsecure_short}} enable CSPM following the steps described [here](link-to-how-to).