---

copyright:
  years:  2023
lastupdated: "2023-05-19"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Terminology
{: #wp-terms}

There are unique terms used in {{site.data.keyword.sysdigsecure_full}}.
{: shortdesc}

Control
:   A _control_ identifies a potential issue or violation within the environment and the solution to remediate the situation.

    A control describes a rule, the code that is run to evaluate it, and a remediation playbook to fix the violation that might be detected. There are different types of controls to address business, security, compliance, and operational requirements. For more information, see [Posture controls](/docs/workload-protection?topic=workload-protection-posture-controls).

Policy
:   A _policy_ is a group of business, security, compliance, and operations _requirements_ representing a compliance standard (for example, PCI 3.2.1), benchmark (for example, CIS Kubernetes 1.5.1) or business policy (for example, My corporation policy v1).

    A policy includes one or more controls to define a compliance standard, a benchmark, or a business policy.

    Policies can be [reviewed and new policies created.](/docs/workload-protection?topic=workload-protection-manage-policies)

Requirement
:   A _requirement_ includes 1 or more controls.

    A requirement exists in a policy and represents a section within the policy that is familiar to compliance officers and auditors.

Requirement group
:   A _requirement group_ defines the hierarchy and structure of controls in a policy. A requirement group consolidates one or more individual requirements within a policy.

Risk acceptance
:   _Risk acceptance_ is the ability to review a violation or vulnerability and acknowledge it without remediating it. Risk acceptance will allow the policy to pass evaluation with the existing violation or vulnerability for a defined period of time.

Zone
:   A _zone_ is a group of resources associated with a customer's business. Zones are defined by a collection of scopes or resource types.
