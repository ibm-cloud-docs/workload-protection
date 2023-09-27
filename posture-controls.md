---

copyright:
  years:  2023
lastupdated: "2023-09-26"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Posture Controls
{: #posture-controls}

You can use the {{site.data.keyword.sysdigsecure_full}} Posture Controls library to see the logic that is used to determine compliance results.
{: shortdesc}

For more information about how an instance of {{site.data.keyword.sysdigsecure_full_notm}} can be integrated with {{site.data.keyword.compliance_short}} to run scans that validate your level of compliance, check out [Connecting Workload Protection](cloud.ibm.com/docs/security-compliance?topic=security-compliance-setup-workload-protection).
{: tip}

A control describes a rule, for example `/etc/docker/certs.d/*/* owned by root:root`, the code that is run to evaluate it, and a remediation playbook to fix the violation that might be detected.

There are different types of controls to address business, security, compliance, and operational requirements.

Posture Controls helps you:

* Ensure that the compliance analysis fits your organization's needs.

* Know what is evaluated.

* Review specific controls and the logic in those controls and remediations.

For more information about compliance, see [**Compliance** views and functions documentation.](/docs/workload-protection?topic=workload-protection-compliance)

Controls are built on the [Open Policy Agent (OPA) engine](https://www.openpolicyagent.org/docs/latest/){: external} that uses the [Rego policy language](https://www.openpolicyagent.org/docs/latest/policy-language/){: external}.

The Posture Controls library shows you the code that is used to create the controls and the inputs they evaluate. You can download this code as a JSON file.


## Accessing Posture Controls
{: #posture-controls-access}

To access the **Posture Controls**, do the following steps:

1. Open the [{{site.data.keyword.sysdigsecure_short}} UI](/docs/workload-protection?topic=workload-protection-launch).

2. Hover over the **Policies** icon ![Policies icon](/images/policies.png "Policies") and click **Controls**. The controls are displayed.

   You can filter the list by:

   Severity
   :   The severity that is assigned to the control: high (H), medium (M), or low (L).

   Type
   :   The infrastructure type. For example, cluster, host, identity, or resource.

   Target
   :   The specfic platforms or distributions that a control evaluates resources against.

   You can also search on any word, or part of a word, in the control name.

   Multiple filters can be specified to create more specific filter expressions.
   {: tip}

3. Click a control to work with it. The control details are displayed.

   The details displays:

   * The control title.

   * The control severity.

   * The control type. For example, `Host`.

   * The control author. The author is `Sysdig` for {{site.data.keyword.sysdigsecure_full_notm}} provided controls.

   * A description of the control.

   * The policies that are linked to the control.

     Hovering over a policy displays the policy details. For example, the requirement number for the compliance standard.

4. Click the **Code** tab.

   The code used to evaluate the objects and how the evaluation rules are structured is displayed. The code is shown in [Rego format.](https://www.openpolicyagent.org/docs/latest/policy-language/){: external} Where appropriate, required inputs are included.

   You can copy or download this code to use as a template for other policies.
   {: tip}

5. Click the **Remediation Playbook** tab.

   The steps to resolve the failing control are displayed.
