---

copyright:
  years:  2023
lastupdated: "2023-09-26"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Understanding Kubernetes Security Posture Management (KSPM)
{: #kspm}

{{site.data.keyword.sysdigsecure_full}} implements Kubernetes security posture management (KSPM). You need to understand KSPM and how it applies to monitoring your Kubernetes environment.
{: shortdesc}

For more information about how an instance of {{site.data.keyword.sysdigsecure_full_notm}} can be integrated with {{site.data.keyword.compliance_short}} to run scans that validate your level of compliance, check out [Connecting Workload Protection](cloud.ibm.com/docs/security-compliance?topic=security-compliance-setup-workload-protection).
{: tip}

Cloud security posture management, or CSPM, uses automation to detect and remediate security and compliance issues in the cloud.

The relationship between Kubernetes security posture management and cloud security posture management is subjective. You can argue that KSPM is one component of CSPM, given that Kubernetes environments often run in the cloud.

Or, you can view KSPM as a distinct domain, because Kubernetes doesn’t always run in the cloud. That is, it can be deployed in on-premises environments as well. Also, the types of resources and configurations that KSPM validates, such as Kubernetes RBAC policies, are different from the resources that CSPM can protect. CSPM can protect cloud IAM policies, cloud networking configurations, and so on.

Regardless of how you choose to think about the relationship between KSPM and CSPM, what is important is understanding that KSPM addresses the security and compliance risks of Kubernetes. CSPM helps manage risks in other types of cloud-native environments. If you use Kubernetes, you need a security tool that offers specific KSPM functions such as {{site.data.keyword.sysdigsecure_full_notm}}.

## What is Kubernetes security posture management?
{: #whatis_kspm}

Kubernetes security posture management, or KSPM, is the use of security automation tools to discover and fix security and compliance issues within a Kubernetes component.

For example, KSPM can detect misconfigurations in a Kubernetes RBAC role definition that grants users permissions that they should not have. For example, the ability to create new pods. Or, a KSPM tool can alert you to an insecure Kubernetes network configuration that allows communication between pods in different namespaces. Communication between pods in different namespaces would not be a typical setting.

## Why is Kubernetes security posture management important?
{: #why_kspm}

As part of a broader Kubernetes security strategy, KSPM addresses several important security considerations.

### Identifying possible human errors and oversights
{: #why_kspm_1}

KSPM is a solution for checking the security of the configurations that you use to govern Kubernetes resources. The risk that human error or oversight can result in configurations that are not as secure as they ideally would be.

KSPM helps teams find and fix these mistakes before they lead to breaches.

### Managing security as clusters evolve
{: #why_kspm_2}

Kubernetes is a rapidly evolving technology, and configurations that are secure for one version of Kubernetes might stop being secure if you upgrade to a new version.

For instance, Kubernetes announced in 2021 that pod security policies, which were a critical resource for enforcing certain types of access control over pods, are deprecated. Current versions of Kubernetes still enforce pod security policies, but support ends with version 1.25. If you are still using pod security policies when you upgrade to version 1.25, a KSPM tool, such as {{site.data.keyword.sysdigsecure_full_notm}}, can alert you to the fact that Kubernetes is ignoring your policies. KSPM can alert you to replace outdated policies with tools such as Kubernetes security contexts or custom admissions controllers.

### Validating third-party configurations
{: #why_kspm_3}

Kubernetes is a system where teams routinely borrow or import resources from upstream. For example, you can pull container images from a public Docker Hub registry or apply a deployment file from GitHub. The third-party developers who create those resources might or might not follow the same security conventions as your own team.

KSPM offers a way of scanning third-party resources for possible security issues. In turn, you can take advantage of the rich resources that the Kubernetes community offers while also managing the associated security risks.

### Enforcing Kubernetes compliance
{: #why_kspm_4}

Because KSPM uses policy engines to evaluate configurations and identify risks, it lends itself well to scenarios where businesses need to meet specific compliance requirements.

By writing policies that ensure that data managed or accessed by Kubernetes is stored so that it is compliant with frameworks such as HIPAA or the GDPR, you can automate compliance management.

## How does Kubernetes security posture management Work?
{: #how_kspm}

Although different tools can take a different approach to KSPM, KSPM workflows include the following key steps.

### Define Security Rules
{: #how_kspm_1}

KSPM tools are powered by policies that define security and compliance risks. Most KSPM tools come with a built-in set of policies, and admins can define their own.

### Scan configurations
{: #how_kspm_2}

Using security and compliance rules, KSPM tools automatically scan a Kubernetes environment. For each scanned resource, configurations that violate the predefined rules are identified.

Ideally, configuration scanning takes place continuously so that risks are identified in real time whenever a new configuration is introduced or an existing one is updated.

### Detect, assess, and alert
{: #how_kspm_3}

When a policy violation is detected, KSPM tools assess the severity level of the violation, then generates an alert or notification if the severity level merits immediate notification. Minor issues might be recorded in a log that the team can address later.

### Remediate
{: #how_kspm_4}

When a notice of a security or compliance policy violation is received, admins investigate and remediate the problem. In certain cases, it might be possible with advanced KSPM tools, such as {{site.data.keyword.sysdigsecure_full_notm}} to remediate issues automatically.

## Getting the most out of KSPM
{: #bestuse_kspm}

Deploying a KSPM tool to help monitor your Kubenetes environments is only the first step in mitigating security and compliance risks. Teams can follow some steps to get the most value out of KSPM.

### Scan continuously
{: #bestuse_kspm_1}

Continuously scan configurations. Kubernetes environments tend to change constantly as containers are redeployed, namespaces added or modified, users and service accounts created or removed, and so on.

Continuous scanning ensures that you identify security issues soon after they occur.

### Keep your rules up to date
{: #bestuse_kspm_2}

Kubernetes security and compliance risks are always evolving. So are the Kubernetes configurations themselves. If your KSPM tools rely on rules that were designed for an earlier version of Kubernetes, or that are outdated, they might not be able to detect the newest risks.

Avoid this problem by using policy rules that are continuously updated as Kubernetes changes.

### Categorize risks
{: #bestuse_kspm_3}

Not all security and compliance risks in Kubernetes are equally serious. For example, a container that is allowed to run in privileged mode is likely to be a more serious risk than a user who was mistakenly given list permissions for pods.

To help your team identify and respond to the most serious risks first, use KSPM tools, such as {{site.data.keyword.sysdigsecure_full_notm}}, and policies that can detect risks and categorize them by severity level.

### Don’t rely on KSPM alone
{: #bestuse_kspm_4}

KSPM is one part in a Kubernetes security strategy, but it isn't the only one. KSPM is not a substitute for runtime security, which helps detect active threats within your environment. Nor does KSPM address risks such as malware inside containers, which is a threat that a container image scanning can handle.

You must deploy a broad set of security tools for Kubernetes, such as {{site.data.keyword.sysdigsecure_full_notm}}. As part of a broader Kubernetes security strategy, KSPM allows teams to validate the security of Kubernetes configurations to find and remediate mistakes that can trigger a breach. By running continuous, automatic scans of Kubernetes configurations, admins can mitigate one of the most common areas of attack, human error. At the same time, you can automate compliance in even the most complex Kubernetes clusters.
