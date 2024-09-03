---

copyright:
  years:  2023, 2024
lastupdated: "2024-09-03"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# About IBM Cloud Security Posture Management (CSPM)
{: #about}

In {{site.data.keyword.cloud_notm}}, {{site.data.keyword.sysdigsecure_full}} automates compliance checks for [{{site.data.keyword.cloud_notm}} Framework for Financial Services](/docs/framework-financial-services?topic=framework-financial-services-about), Digital Operational Resilience Act (DORA), CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark, PCI and many other industry related or best practices standards. With a detailed inventory of your {{site.data.keyword.cloud_notm}} resources and prioritization based on full context it facilitates the resolution and management of collected violations.

The {{site.data.keyword.sysdigsecure_short}} posture module supports compliance validation on {{site.data.keyword.cloud_notm}}, multi-cloud environments (Amazon Web Services, Azure and Google Cloud), inside hosts, virtual machines (VSIs for VPC, VMware, PowerVS and IBM Z with Linux), Kubernetes, and OpenShift.
{: note}

The posture module brings many features for your CSPM in your hybrid environments:

- Unified and centralized view to manage security and compliance of applications, workloads and infrastructure running on {{site.data.keyword.cloud_notm}}, in other cloud providers and on-premise, covering managed services, hosts, virtual machines and containers and Kubernetes or OpenShift clusters.

- Many predefined frameworks such as Financial Services, PCI, DORA, CIS or NIST allow to implement and validate the controls that are required to meet industry standards and laws.

- Inventory of all your cloud assests (compute resources, managed services, identities, and entitlements) and hosts, virtual machines, clusters and all Kubernetes or OpenShift resources, whether they are in the cloud or on-premises.

- A risk acceptance flow for removing the violation from the failed controls with options for the reason and expiration period for the acceptance. Risk can be accepted at one resource level or globally for all resources from one control.

- Detailed remediation instructions to fix failing controls.

- Ability to create custom policies, controls, and control parameters.

## Available pre-defined policies for IBM Cloud CSPM in {{site.data.keyword.sysdigsecure_short}}

The following posture policies are available for you to use to implement CSPM for your {{site.data.keyword.cloud_notm}} resources:

| Policy  | Description |
|:---------|:------------|
| CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark | Validate that your resource configurations meet the baseline requirements that are identified by the Center for Internet Security. |
| {{site.data.keyword.cloud_notm}} Framework for Financial Services | [{{site.data.keyword.cloud_notm}} for Financial Services™](/docs/framework-financial-services?topic=framework-financial-services-about) is an open platform that brings together independent software vendors (ISVs), Software as a Service (SaaS) providers, and financial services institutions in a single ecosystem. In this secure cloud platform, you can rapidly develop and share innovative applications, APIs, data, and content to meet the unique business needs of your financial institution.  \n \n Through the [{{site.data.keyword.framework-fs_full}}](/docs/framework-financial-services?topic=framework-financial-services-about), you can access a unified set of security and compliance controls, which was built specifically for and with the financial services industry. To address your evolving needs as a financial institution, IBM continuously validates these controls with global Councils of CSOs, CTOs, and CIOs from major banks, insurance providers, and regulatory advisors.  \n \n The {{site.data.keyword.cloud_notm}} for Financial Services profile provides you with a set of pre-configured automated goals that are mapped to the [{{site.data.keyword.framework-fs_full}} control requirements](/docs/framework-financial-services?topic=framework-financial-services-about#framework-control-requirements). The results of these tests help you validate compliance when you are using one of the [references architectures](/docs/framework-financial-services?topic=framework-financial-services-reference-architecture-overview) for the {{site.data.keyword.cloud_notm}} for Financial Services. |
| Digital Operational Resilience Act (DORA) - Regulation (EU) 2022/2554 | The Digital Operational Resilience Act (Regulation (EU) 2022/2554) solves an important problem in the EU financial regulation. Before DORA, financial institutions managed the main categories of operational risk mainly with the allocation of capital, but they did not manage all components of operational resilience. After DORA, they must also follow rules for the protection, detection, containment, recovery, and repair capabilities against ICT-related incidents. DORA explicitly refers to ICT risk and sets rules on ICT risk-management, incident reporting, operational resilience testing and ICT third-party risk monitoring. This Regulation acknowledges that ICT incidents and a lack of operational resilience have the possibility to jeopardise the soundness of the entire financial system, even if there is adequate capital for the traditional risk categories. |
| Esquema Nacional de Seguridad (ENS) High | By provision of a Spanish law, Spanish citizens have a legal right to access government services electronically. Governed by Royal Decree 3/2010, the Esquema Nacional de Seguridad (ENS) (National Security Framework) aims to establish a security policy for the use of electronic media. Inclusive of cloud computing services, ENS defines basic principles and minimum requirements for the protection of information. |
| AI ICT guardrails | The AI ICT guardrails provides a predefined list of infrastructure and data controls, required to handle AI and Generative AI (GenAI) workloads. These controls include AI specific elaborations across control categories like risk and compliance management, unified infrastructure security and performance, application and workload protection, data protection, identity and access management, logging, and monitoring. This list of controls is to be used in conjunction with the security baseline of the organization. |
| C5:2020 (Cloud Computing Compliance Criteria Catalog) | The Cloud Computing Compliance Controls Catalog (C5), created by the German Federal Office for Information Security (Bundesamt für Sicherheit in der Informationstechnik, or BSI) outlines requirements that cloud service providers must meet in order to provide a minimum security level for their services. |
| SOC 2 | SOC 2 is a voluntary compliance standard for service organizations, developed by the American Institute of CPAs (AICPA). Its intent is to ensure the safety and privacy of user data. It outlines the five trust service principles of security, availability, processing integrity, confidentiality, and privacy of customer data as a framework for safeguarding data. SOC 2 applies to any technology service provider or SaaS company that handles or stores customer data. Third-party vendors, other partners, or support organizations that those firms work with should also maintain SOC 2 compliance to ensure the integrity of their data systems and safeguards. |
| ISMAP (Information System Security Management and Assessment Program) | The Information System Security Management and Assessment Program (ISMAP) aims to secure the security level of the government's cloud service procurement by evaluating and registering cloud services that meet the security requirements of the government in advance, thereby contributing to the smooth introduction of cloud services. |
| PCI DSS (Payment Card Industry Data Security Standard) v4.0.0 | The Payment Card Industry Data Security Standard (PCI DSS) was developed to encourage and enhance payment card account data security and facilitate the broad adoption of consistent data security measures globally. PCI DSS provides a baseline of technical and operational requirements designed to protect account data. While specifically designed to focus on environments with payment card account data, PCI DSS can also be used to protect against threats and secure other elements in the payment ecosystem. |
{: caption="Table 1. Available predefined policies" caption-side="top"}

All other posture policies apply to other environments such as AWS, Azure, GCP, Kubernetes, OpenShift, or hosts.

## Next steps
{: #about-next}

To get the most of {{site.data.keyword.sysdigsecure_short}} enable CSPM following the steps described in [Implementing CSPM (Cloud Security Posture Management) for {{site.data.keyword.cloud_notm}} using the UI and CLI](/docs/workload-protection?topic=workload-protection-cspm-implement).
