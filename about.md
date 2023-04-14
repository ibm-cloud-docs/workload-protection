---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# About {{site.data.keyword.cloud_notm}} Security and Compliance
{: #about}

In {{site.data.keyword.cloud_notm}}, {{site.data.keyword.compliance_full}} is a unified and centralize framework to manage the security and compliance of applications, workloads and infrastructure in {{site.data.keyword.cloud_notm}}, in other clouds, and on-prem. It includes a workload protection platform (WPP) that focuses on management and security controls for workloads. It also includes a compliance platform (CP) that focuses on management and compliance  controls that are required to meet industry standards and laws. Both platforms offer alerting on violations, and assist with remediation tasks.
{: shortdesc}


Cloud Security defines the collection of policies and controls, practices, and technologies that are designed to address unauthorized access, online attacks, and threats. For more information, see [An overview of cloud security](https://www.ibm.com/topics/cloud-security).

Cloud Compliance defines the collection of policies and controls, practices, and technologies that are designed to address industry regulatory standards, and national and international laws.

Across all industries, in particluar highly regulated industries such as financial services, achieving continuous security and compliance within a cloud environment is an important step toward protecting resources, data and workloads. By default, {{site.data.keyword.cloud_notm}} follow best practices for security and compliance, and take active steps to protect the integrity of their servers and services. But what else can you do to protect your infrastructure and your workloads?

You can use the {{site.data.keyword.sysdigsecure_full_notm}} service to protect and gain visibility of resources, data, applications, and workloads across multiple environments. You can manage workloads and resources that run on {{site.data.keyword.cloud_notm}}, on other clouds, and on-prem. You can use this service to secure your builds, detect and respond to runtime threats, and continuously manage cloud configurations, permissions, and compliance.

The {{site.data.keyword.sysdigsecure_full_notm}} service is a cloud workload protection tool (CWPT) that helps you monitor and protect your organization. Includes Cloud security posture management (CSPM), Kubernetes Security Posture Management (KSPM) and more. Use cloud security posture management features to secure the infrastructure where workloads are deployed. Use Kubernetes Security Posture Management features to secure Kubernetes clusters or Openshift clusters, and the workloads running within it.
{: note}

{{site.data.keyword.sysdigsecure_full_notm}} main goal is to provide the tools that will help you keep your organization secure and able to resist threats and attacks, while making sure that workloads are deployed successfully.
{: note}


## Cloud security posture management (CSPM)
{: #about-cspm}

Cloud security posture management (CSPM) is a framework that includes the policies and controls, the practices, and the technologies to detect and remediate security issues, and compliance risks across multi-cloud environments in your organization. It is focused on securing cloud infrastructures where workloads are deployed. In addition, it addresses security and compliance of Infrastructure as a Service (IaaS), Software as a Service (SaaS), and Platform as a Service (PaaS).

The {{site.data.keyword.sysdigsecure_full_notm}} service includes CSPM functionality to continuously monitor infrastructures in your organization where workloads are deployed.

The {{site.data.keyword.sysdigsecure_full_notm}} service inspects cloud environments across multiple environments to continuously:

- Scan, detect and alert of misconfigurations, malware, secrets, and software configuration vulnerabilities. Empower DevOps to fix them fast.

- Provide fixes and guidance on how to remediate security findings.

- Map misconfigurations in production to infrastructure as code (IaC) manifests.

    Fix violations by opening a pull request to the source file.

    The {{site.data.keyword.sysdigsecure_short}} is integrated with Git.

- Provide control over cloud infrastructure configurations and ensure consistent implementation of policies across multiple cloud providers.

    Use out-of-the-box compliance controls.

    Create customized security policies that align with your security mandates.

    Duplicate an existing security policy and turn on/off controls, or create a new ones from scratch.

- Monitor for suspicious activity and threats.

    Perform risk assessments of your infrastructure and workloads by checking policies and controls that are included in standard frameworks such as CIS, PCI, NIST.

    Enforce compliance with controls using policy as code based on OPA.

- Monitor all suspicious activity performed by privileged users.

- Integrate with DevOps tools to streamline the incident response process.

- Show proof of your compliance through audit logs and container forensics data.




## Kubernetes Security Posture Management (KSPM)
{: #about-kspm}


Kubernetes security posture management, or KSPM, is the use of security automation tools to discover and fix security and compliance issues within a Kubernetes component.

- KSPM provides processes and technologies to help secure a Kubernetes cluster or an Openshift cluster, and the workloads running within it.

- KSPM continuously analyzes and evaluates the security of cluster components and their configurations, identifies potential vulnerabilities, and monitors for and responds to security incidents.

KSPM is one part in a Kubernetes security strategy, but it isn't the only one. KSPM is not a substitute for runtime security, which helps detect active threats within your environment. Nor does KSPM address risks such as malware inside containers, which is a threat that a container image scanning can handle.

You must deploy a broad set of security tools for Kubernetes, such as {{site.data.keyword.sysdigsecure_full_notm}}. As part of a broader Kubernetes security strategy, KSPM allows teams to validate the security of Kubernetes configurations to find and remediate mistakes that can trigger a breach. By running continuous, automatic scans of Kubernetes configurations, admins can mitigate one of the most common areas of attack, human error. At the same time, you can automate compliance in even the most complex Kubernetes clusters.

For more information, see [About KSPM](/docs/workload-protection?topic=workload-protection-kspm).
