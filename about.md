---

copyright:
  years:  2023, 2024
lastupdated: "2024-01-17"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# About Posture Management
{: #about}

For more information about how an instance of {{site.data.keyword.sysdigsecure_full_notm}} can be integrated with {{site.data.keyword.compliance_short}} to run scans that validate your level of compliance, check out [Connecting Workload Protection](/docs/security-compliance?topic=security-compliance-setup-workload-protection).
{: tip}

Posture Management is a practice that you can use to keep your organization safe on-prem and cross-cloud. In {{site.data.keyword.cloud}}, you can use {{site.data.keyword.sysdigsecure_short}}, a unified and centralized framework to manage the security and compliance of applications, workloads, and infrastructure in {{site.data.keyword.cloud_notm}}, in other clouds, and on-prem.
{: shortdesc}

Posture Management provides the framework that includes controls, guidelines, benchmarks, and standards for managing infrastructures, including Infrastructure as a Service (IaaS), Software as a Service (SaaS), and Platform as a Service (PaaS). Posture Management helps you in the identification and remediation of risk within your organization.

Cloud Security defines the collection of policies and controls, practices, and technologies that are designed to address unauthorized access, online attacks, and threats. For more information, see [An overview of cloud security](https://www.ibm.com/topics/cloud-security).

Cloud Compliance defines the collection of policies and controls, practices, and technologies that are designed to address industry regulatory standards, and national and international laws.

Across all industries, in particluar in highly regulated industries such as financial services, achieving continuous security and compliance within a cloud environment is an important step toward protecting resources, data and workloads. By default, {{site.data.keyword.cloud_notm}} follows best practices for security and compliance, and takes active steps to protect the integrity of their servers and services. But what else can you do to protect your infrastructure and your workloads?

You can use the {{site.data.keyword.sysdigsecure_full_notm}} service to protect and gain visibility to resources, data, applications, and workloads across multiple environments. You can manage workloads and resources that run on {{site.data.keyword.cloud_notm}}, on other clouds, and on-prem. You can use this service to secure your builds, detect and respond to runtime threats, and continuously manage cloud configurations, permissions, and compliance.

{{site.data.keyword.sysdigsecure_full_notm}} offers functionality to protect workloads and get deep cloud and container visibility. It has features to implement and manage security and compliance posture management, vulnerability scanning, forensics, threat detection and blocking, and more. It offers a workload protection platform (WPP) that focuses on management and security controls for workloads. It also includes a compliance platform (CP) that focuses on management and compliance controls that are required to meet industry standards and laws. Both platforms offer alerting on violations, and assist with remediation tasks.

The {{site.data.keyword.sysdigsecure_full_notm}} service is a cloud workload protection tool (CWPT) that helps you monitor and protect your organization. {{site.data.keyword.sysdigsecure_full_notm}} includes Cloud Security Posture Management (CSPM), Kubernetes Security Posture Management (KSPM) and more.

Use **Cloud security posture management (CSPM)** features to secure the infrastructure where workloads are deployed.
{: note}

Use **Kubernetes Security Posture Management (KSPM)** features to secure Kubernetes clusters or {{site.data.keyword.redhat_openshift_notm}} clusters, and the workloads running within them.
{: note}

The main goal of {{site.data.keyword.sysdigsecure_full_notm}} is to provide the tools that will help you keep your organization secure and able to resist threats and attacks, while making sure that workloads are successfully deployed.

## Cloud Security Posture Management (CSPM)
{: #about-cspm}

Cloud Security Posture Management (CSPM) is a framework that includes the policies and controls, the practices, and the technologies to detect and remediate security issues, and compliance risks across multi-cloud environments in your organization. It is focused on securing cloud infrastructures where workloads are deployed. In addition, it addresses security and compliance of Infrastructure as a Service (IaaS), Software as a Service (SaaS), and Platform as a Service (PaaS).

The {{site.data.keyword.sysdigsecure_full_notm}} service includes CSPM functionality to continuously monitor infrastructures in your organization where workloads are deployed.

The {{site.data.keyword.sysdigsecure_full_notm}} service inspects cloud environments across multiple environments to continuously:

- Scan, detect and alert about misconfigurations, malware, secrets, and software configuration vulnerabilities. Empower DevOps to fix these issues fast.

- Provide fixes and guidance on how to remediate security findings.

- Map misconfigurations in production to infrastructure as code (IaC) manifests.

    Fix violations by opening a pull request to the source file.

    The {{site.data.keyword.sysdigsecure_short}} is integrated with Git.
    {: note}

- Provide control over cloud infrastructure configurations and ensure consistent implementation of policies across multiple cloud providers.

    Use out-of-the-box compliance controls.

    Create customized security policies that align with your security mandates.

    Duplicate an existing security policy and turn on and off controls, or create a new ones from scratch.

- Monitor for suspicious activity and threats.

    Perform risk assessments of your infrastructure and workloads by checking policies and controls that are included in standard frameworks such as CIS, PCI, NIST.

    Enforce compliance with controls using policy as code based on OPA.

- Monitor all suspicious activity performed by privileged users.

- Integrate with DevOps tools to streamline the incident response process.

- Show proof of your compliance through audit logs and container forensics data.

## Kubernetes Security Posture Management (KSPM)
{: #about-kspm}


Kubernetes Security Posture Management, or KSPM, is the use of security automation tools to discover and fix security and compliance issues within a Kubernetes component.

- KSPM provides processes and technologies to help secure a Kubernetes cluster or a {{site.data.keyword.redhat_openshift_notm}} cluster, and the workloads running within it.

- KSPM continuously analyzes and evaluates the security of cluster components and their configurations, identifies potential vulnerabilities, and monitors for, and responds to, security incidents.

KSPM is one part in a Kubernetes security strategy, but it isn't the only one. KSPM is not a substitute for runtime security, which helps detect active threats within your environment. Nor does KSPM address risks such as malware inside containers, which is a threat that  container image scanning can handle.

You must deploy a broad set of security tools for Kubernetes. Included in your security tools can be {{site.data.keyword.sysdigsecure_full_notm}}. As part of a broader Kubernetes security strategy, KSPM allows teams to validate the security of Kubernetes configurations to find and remediate mistakes that can trigger a breach. By running continuous, automatic scans of Kubernetes configurations, admins can mitigate one of the most common areas of attack, human error. At the same time, you can automate compliance in even the most complex Kubernetes clusters.

For more information, see [About KSPM](/docs/workload-protection?topic=workload-protection-kspm).


## Network policies for containerized workloads
{: #about-nw}

When clients provision a cluster, they can choose a networking setup so that certain cluster components can communicate with each other and with networks or services outside of the cluster. Examples of [networking configurations](https://cloud.ibm.com/docs/containers?topic=containers-plan_vpc_basics) are:

* Worker-to-worker
* Worker-to-master
* User-to-master
* Worker communication to other services or networks
* External communication to apps that run on worker nodes.

Clusters on Virtual Private Clouds (VPCs) run on secure, isolated virtual networks where traffic flow to and from worker nodes is controlled by applying rules defined through security groups (SGs). Traffic flow to and from the cluster subnets is controlled by ACLs. Clients can define container network policies to restrict egress and ingress traffic and communication between applications.

With the [Network Security Policy tool](/docs/workload-protection?topic=workload-protection-netsec_policy) that is available through the {{site.data.keyword.sysdigsecure_full_notm}} service, clients can generate and fine-tune Kubernetes network policies based on the traffic allowed or denied, and track ingress and egress communication. For example, you can configure a "least-privilege" policy to protect your workloads or view existing network policies that have been applied to you workloads.

{{site.data.keyword.sysdigsecure_short}} leverages native Kubernetes features and doesn't require any additional networking requirements other than the Container Network Interface (CNI). Through the UI, clients can view which policies are being applied in real time.
