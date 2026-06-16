---

copyright:
  years: 2023, 2026
lastupdated: "2026-06-16"

keywords: compliance, posture management, security posture, compliance evaluation, remediation, controls, policies, zones, CSPM, KSPM

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Analyzing compliance postures from detection to remediation
{: #compliance}

{{site.data.keyword.sysdigsecure_full}} provides comprehensive compliance posture management capabilities that help security teams, compliance officers, and DevOps engineers continuously monitor, evaluate, and improve their security posture across cloud environments. The platform enables organizations to detect compliance violations, understand their security posture, and drive remediation through to resolution.
{: shortdesc}

Information about your compliance posture is included in an [inventory](https://docs.sysdig.com/en/docs/sysdig-secure/inventory/){: external}, which enhances resource visibility and provides full-context prioritization. This information helps you drive remediation and resolution of compliance violations. To access your inventory and other compliance-related information, open the {{site.data.keyword.sysdigsecure_short}} UI. In the console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Security > Compliance** and click the name of your instance of {{site.data.keyword.sysdigsecure_short}}. Then, click **Open dashboard** to open the {{site.data.keyword.sysdigsecure_short}} UI. 
{: note}

## How compliance posture management works
{: #compliance-how-it-works}

{{site.data.keyword.sysdigsecure_short}} evaluates the resources in your [zones](https://docs.sysdig.com/en/sysdig-secure/zones/){: external} against compliance policies. Any violations are collected and displayed as tiles on the **Compliance** page in the {{site.data.keyword.sysdigsecure_short}} UI. This evaluation is performed once daily to provide up-to-date compliance status.

You can use {{site.data.keyword.sysdigsecure_short}} predefined policies or [create custom policies](https://docs.sysdig.com/en/sysdig-secure/manage_posture_policies/#create-a-custom-policy){: external} tailored to your organization's specific requirements. When evaluating violations, you can select individual resources to see their associated list of violations, enabling targeted remediation efforts.

### Key concepts
{: #compliance-concepts}

The compliance workflow consists of the following key components:

Zones
:   Logical groupings of resources that represent different parts of your infrastructure. The default _Entire Infrastructure_ zone is automatically created by {{site.data.keyword.sysdigsecure_short}}, and you can define custom zones to match your organizational structure. Zones are defined by a collection of scopes or resource types. 

Policies
:   Collections of requirements that define a compliance standard. A policy includes one or more controls to define that compliance standard. Policies can be based on industry frameworks or custom organizational requirements.

Requirements
:   Specific compliance criteria that must be met. Each requirement consists of one or more controls.

Controls
:   Identifies a potential issue or violation within the environment and the solution to remediate the problem. Different types of controls are used to address business, security, compliance, and operational requirements. 

The **Compliance** overview page displays key posture performance indicators for each policy applied to your zones. For more information, see [Understanding the Compliance UI](https://docs.sysdig.com/en/sysdig-secure/compliance/#understand-the-compliance-ui){: external}. 
{: tip}

## Compliance workflow overview
{: #compliance-workflow}

The typical compliance posture management workflow follows these stages:

1. Detection and assessment. {{site.data.keyword.sysdigsecure_short}} scans your environment daily and evaluates resources against defined policies. {{site.data.keyword.sysdigsecure_short}} identifies violations and categorizes them by severity, providing a comprehensive view of your compliance posture.
1. Analysis and prioritization. Security and compliance teams can review high-level posture performance indicators for each policy applied to their zones. By selecting a policy, teams can see detailed results, including failing requirements, associated controls, and affected resources. 
1. Evaluation and decision making. When reviewing violations, [teams can examine the control pane](https://docs.sysdig.com/en/sysdig-secure/compliance-findings/#drill-down-to-the-control-pane){: external} to understand the hierarchy of requirements and controls. Each item indicates whether it's passing or failing.
1. Remediation. {{site.data.keyword.sysdigsecure_short}} provides multiple remediation options to address compliance violations. For more information, see [Evaluate and Remediate](https://docs.sysdig.com/en/sysdig-secure/compliance-findings/#drill-down-to-the-control-pane){: external}.
1. Reporting and documentation. Organizations can generate [compliance reports](https://docs.sysdig.com/en/sysdig-secure/compliance/#policy-compliance-report){: external} that can be downloaded from the UI or accessed via API. These reports can be shared with development teams, executives, auditors, and other stakeholders who require compliance status information.
1. Source detection and patching. When [Git integration is implemented](https://docs.sysdig.com/en/sysdig-secure/github-action-integration/){: external}, {{site.data.keyword.sysdigsecure_short}} scans and analyzes the manifests from your defined Git sources daily or whenever a new Git source is added. The system determines which resources are declared in your source files and attempts to match discovered resources with deployed and evaluated resources.

## Use cases by role
{: #compliance-use-cases}

Different organizational roles benefit from compliance posture management in specific ways:

### Compliance and security teams
{: #compliance-security-teams}

Compliance and security team members use the compliance feature to:

* Check the current compliance status of business zones against predefined policies.
* Demonstrate to auditors the compliance status of their business zone at a specific point in time.
* Create reports of compliance status to share with auditors and management teams.
* Understand the magnitude of the compliance gap and track improvement over time.
* Monitor trends in compliance posture through historical data visualization.

### DevOps engineers
{: #compliance-devops}

DevOps team members use the compliance feature to:

* Identify compliance violations for predefined policies on their business zones.
* Manage violations according to their severity, prioritizing high-severity issues.
* Efficiently fix violations using automated patches or pull requests.
* Document exceptions and acceptable risks according to organizational risk management policies.
* Integrate compliance checks into their CI/CD pipelines.

### Cloud architects
{: #compliance-architects}

Cloud architects use the compliance feature to:

* Design infrastructure that meets compliance requirements from the start.
* Understand which controls apply to different resource types and configurations.
* Evaluate the compliance impact of architectural decisions.
* Ensure new deployments align with organizational security policies.
