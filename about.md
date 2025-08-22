---

copyright:
  years:  2023, 2025
lastupdated: "2025-08-22"

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

- Capability to integrate all your {{site.data.keyword.sysdigsecure_short}} accounts and enterprise seamlessly. 

## Available pre-defined policies for IBM Cloud CSPM in {{site.data.keyword.sysdigsecure_short}}
{: #about-available-policies}

The following posture policies are available for you to use to implement CSPM for your {{site.data.keyword.cloud_notm}} resources:

| Policy  | Description |
|:---------|:------------|
| AI ICT guardrails | The AI ICT guardrails provides a predefined list of infrastructure and data controls, required to handle AI and Generative AI (GenAI) workloads. These controls include AI specific elaborations across control categories like risk and compliance management, unified infrastructure security and performance, application and workload protection, data protection, identity and access management, logging, and monitoring. This list of controls is to be used in conjunction with the security baseline of the organization. |
| AI Security Guardrails 2.0 | The AI Security Guardrails provides a list of controls for the full stack including AI Applications, Models, Data, and infrastructure layers, required to handle AI and Generative AI(GenAI) workloads. These controls include AI specific elaborations across control categories like AI Governance, AI App Protection, AI Model Lifecycle, Data Classification and infrastructure security and operational resiliency.|
| Australian Government Information Security Manual (ISM) 2022 | The Cloud Controls Matrix Template is intended for use by Infosec Registered Assessors Program (IRAP) assessors to capture the implementation of controls from the Information Security Manual (ISM) by a Cloud Service Provider (CSP). In doing so, the CCM template provides indicative guidance on the scoping of security assessments, however, it should be noted that the guidance is not definitive and should be interpreted by IRAP assessors in the context of the services being assessed. The CCM template also captures the ability for consumers to implement controls for services built upon a CSP's services by identifying where they are responsible for configuring their own services in accordance with the ISM. |
| BSI-Standard 200-1: Information Security Management | The BSI-Standard 200-1, issued by the German Federal Office for Information Security (BSI), provides comprehensive guidelines for establishing and maintaining an effective information security management system (ISMS). It outlines the fundamental principles and practices necessary for identifying, managing, and mitigating information security risks within an organization. The standard is structured to be applicable across various industries and sectors, ensuring that organizations can protect their information assets effectively, comply with legal and regulatory requirements, and enhance their overall security posture. |
| C5:2020 (Cloud Computing Compliance Criteria Catalog) | The Cloud Computing Compliance Controls Catalog (C5), created by the German Federal Office for Information Security (Bundesamt für Sicherheit in der Informationstechnik, or BSI) outlines requirements that cloud service providers must meet in order to provide a minimum security level for their services. |
| CCPA (California Consumer Privacy Act) | The California Consumer Privacy Act (CCPA) is a data privacy law that provides California consumers with a number of privacy protections, including right to access, delete, and opt-out of the “sale” of their personal information. Starting January 1, 2020, businesses that collect California residents’ personal information and meet certain thresholds (e.g., revenue, volume of data processing) will need to comply with these obligations. |
| CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark | Validate that your resource configurations meet the baseline requirements that are identified by the Center for Internet Security. |
| Cloud Security Alliance (CSA) Cloud Controls Matrix (CCM) | The CSA Cloud Controls Matrix (CCM) is a cybersecurity control framework for cloud computing.It is composed of 197 control objectives that are structured in 17 domains covering all key aspects of cloud technology. It can be used as a tool for the systematic assessment of a cloud implementation, and provides guidance on which security controls should be implemented by which actor within the cloud supply chain. The controls framework is aligned to the CSA Security Guidance for Cloud Computing, and is considered a de-facto standard for cloud security assurance and compliance. |
| Digital Operational Resilience Act (DORA) - Regulation (EU) 2022/2554 | The Digital Operational Resilience Act (Regulation (EU) 2022/2554) solves an important problem in the EU financial regulation. Before DORA, financial institutions managed the main categories of operational risk mainly with the allocation of capital, but they did not manage all components of operational resilience. After DORA, they must also follow rules for the protection, detection, containment, recovery, and repair capabilities against ICT-related incidents. DORA explicitly refers to ICT risk and sets rules on ICT risk-management, incident reporting, operational resilience testing and ICT third-party risk monitoring. This Regulation acknowledges that ICT incidents and a lack of operational resilience have the possibility to jeopardise the soundness of the entire financial system, even if there is adequate capital for the traditional risk categories. |
| DPDP (Digital Personal Data Protection) Act | An Act to provide for the processing of digital personal data in a manner that recognises both the right of individuals to protect their personal data and the need to process such personal data for lawful purposes and for matters connected therewith or incidental thereto. |
| Esquema Nacional de Seguridad (ENS) High | By provision of a Spanish law, Spanish citizens have a legal right to access government services electronically. Governed by Royal Decree 3/2010, the Esquema Nacional de Seguridad (ENS) (National Security Framework) aims to establish a security policy for the use of electronic media. Inclusive of cloud computing services, ENS defines basic principles and minimum requirements for the protection of information. |
| FedRAMP (Federal Risk and Authorization Management Program) High Baseline | Federal Agencies and Cloud Service Providers (CSPs) must implement these security controls, enhancements, parameters, and requirements within a cloud computing environment to satisfy FedRAMP requirements. The security controls and enhancements have been selected from the NIST SP 800-53 Revision 4 catalog of controls. The selected controls and enhancements are for cloud systems designated at the high impact information systems as defined in the Federal Information Processing Standards (FIPS) Publication 199. High Impact data is usually in Law Enforcement and Emergency Services systems, Financial systems, Health systems, and any other system where loss of confidentiality, integrity, or availability could be expected to have a severe or catastrophic adverse effect on organizational operations, organizational assets, or individuals. FedRAMP introduced their High Baseline to account for the government’s most sensitive, unclassified data in cloud computing environments, including data that involves the protection of life and financial ruin. |
| FedRAMP (Federal Risk and Authorization Management Program) LI-SaaS Baseline | Federal Agencies and Cloud Service Providers (CSPs) must implement these security controls, enhancements, parameters, and requirements within a cloud computing environment to satisfy FedRAMP requirements. The security controls and enhancements have been selected from the NIST SP 800-53 Revision 4 catalog of controls. The selected controls and enhancements are for cloud systems designated at the low impact information systems as defined in the Federal Information Processing Standards (FIPS) Publication 199. FedRAMP Tailored was developed to support industry solutions that are low risk and low cost for agencies to deploy and use. Tailored policy and requirements provide a more efficient path for Low Impact-Software as a Service (LI-SaaS) providers. The LI-SaaS Baseline accounts for Low-Impact SaaS applications that do not store personal identifiable information (PII) beyond that is generally required for login capability (i.e. username, password, and email address). Required security documentation is consolidated and the requisite number of security controls needing testing and verification are lowered relative to a standard Low Baseline authorization. While all requirements identified in the FedRAMP Low Baseline are required, FedRAMP Tailored identifies those requirements typically satisfied by a LI-SaaS customer, or underlying service provider, allowing the provider to focus only on relevant requirements. Further, FedRAMP Tailored allows agencies to independently validate only the most important of these requirements. |
| FedRAMP (Federal Risk and Authorization Management Program) Low Baseline | Federal Agencies and Cloud Service Providers (CSPs) must implement these security controls, enhancements, parameters, and requirements within a cloud computing environment to satisfy FedRAMP requirements. The security controls and enhancements have been selected from the NIST SP 800-53 Revision 4 catalog of controls. The selected controls and enhancements are for cloud systems designated at the low impact information systems as defined in the Federal Information Processing Standards (FIPS) Publication 199. Low Impact is most appropriate for CSOs where the loss of confidentiality, integrity, and availability would result in limited adverse effects on an agency’s operations, assets, or individuals. FedRAMP currently has two baselines for systems with Low Impact data: LI-SaaS Baseline and Low Baseline. |
| FedRAMP (Federal Risk and Authorization Management Program) Moderate Baseline | Federal Agencies and Cloud Service Providers (CSPs) must implement these security controls, enhancements, parameters, and requirements within a cloud computing environment to satisfy FedRAMP requirements. The security controls and enhancements have been selected from the NIST SP 800-53 Revision 4 catalog of controls. The selected controls and enhancements are for cloud systems designated at the moderate impact information systems as defined in the Federal Information Processing Standards (FIPS) Publication 199. Moderate Impact systems accounts for nearly 80% of CSP applications that receive FedRAMP authorization and is most appropriate for CSOs where the loss of confidentiality, integrity, and availability would result in serious adverse effects on an agency’s operations, assets, or individuals. Serious adverse effects could include significant operational damage to agency assets, financial loss, or individual harm that is not loss of life or physical. |
| General Data Protection Regulation GDPR | Welcome to gdpr-info.eu. Here you can find the official PDF of the Regulation (EU) 2016/679 (General Data Protection Regulation) in the current version of the OJ L 119, 04.05.2016; cor. OJ L 127, 23.5.2018 as a neatly arranged website. All Articles of the GDPR are linked with suitable recitals. The European Data Protection Regulation is applicable as of May 25th, 2018 in all member states to harmonize data privacy laws across Europe. If you find the page useful, feel free to support us by sharing the project. |
| HIPAA (Health Insurance Portability and Accountability Act) Security Rule | Health Insurance Portability and Accountability Act (HIPAA) Security Rule deals specifically with Electronic Protected Health Information (EPHI). It lays out three types of security safeguards required for compliance: administrative, physical, and technical. For each of these types, the Rule identifies various security standards, and for each standard, it names both required and addressable implementation specifications. Required specifications must be adopted and administered as dictated by the Rule. Addressable specifications are more flexible. Individual covered entities can evaluate their own situation and determine the best way to implement addressable specifications. |
| HITRUST CSF (Common Security Framework) | The HITRUST CSF provides the structure, transparency, guidance, and cross-references to authoritative sources organizations globally need to be certain of their data protection compliance. The initial development of the HITRUST CSF leveraged nationally and internationally accepted security and privacy-related regulations, standards, and frameworks–including ISO, NIST, PCI, HIPAA, and GDPR–to ensure a comprehensive set of security and privacy controls and continually incorporates additional authoritative sources. The HITRUST CSF standardizes these requirements, providing clarity and consistency and reducing the burden of compliance. |
| {{site.data.keyword.cloud_notm}} Framework for Financial Services v1.1 and v2.0| [{{site.data.keyword.cloud_notm}} for Financial Services™](/docs/framework-financial-services?topic=framework-financial-services-about) is an open platform that brings together independent software vendors (ISVs), Software as a Service (SaaS) providers, and financial services institutions in a single ecosystem. In this secure cloud platform, you can rapidly develop and share innovative applications, APIs, data, and content to meet the unique business needs of your financial institution.  \n \n Through the [{{site.data.keyword.framework-fs_full}}](/docs/framework-financial-services?topic=framework-financial-services-about), you can access a unified set of security and compliance controls, which was built specifically for and with the financial services industry. To address your evolving needs as a financial institution, IBM continuously validates these controls with global Councils of CSOs, CTOs, and CIOs from major banks, insurance providers, and regulatory advisors.  \n \n The {{site.data.keyword.cloud_notm}} for Financial Services profile provides you with a set of pre-configured automated goals that are mapped to the [{{site.data.keyword.framework-fs_full}} control requirements](/docs/framework-financial-services?topic=framework-financial-services-about#framework-control-requirements). The results of these tests help you validate compliance when you are using one of the [references architectures](/docs/framework-financial-services?topic=framework-financial-services-reference-architecture-overview) for the {{site.data.keyword.cloud_notm}} for Financial Services. |
| ISMAP (Information System Security Management and Assessment Program) | The Information System Security Management and Assessment Program (ISMAP) aims to secure the security level of the government's cloud service procurement by evaluating and registering cloud services that meet the security requirements of the government in advance, thereby contributing to the smooth introduction of cloud services. |
| Information Technology Security Guidance (ITSG-33) | ITSG-33 was published by the Canadian Centre for Cybersecurity (CCCS) to assist government departments in ensuring security. It includes a catalog of security controls organized into three classes of control families: Technical, Operational, and Management. |
| MITRE ATT&CK for Enterprise | MITRE ATT&CK® is a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations. The ATT&CK knowledge base is used as a foundation for the development of specific threat models and methodologies in the private sector, in government, and in the cybersecurity product and service community. |
| MITRE DEFEND | In project work for our sponsors, we have repeatedly encountered the need for a model that can precisely specify cybersecurity countermeasure components and capabilities. Furthermore, it is necessary that practitioners know not only what threats a capability claims to address, but specifically how those threats are addressed from an engineering perspective, and under what circumstances the solution would work. This knowledge is essential to estimate operational applicability, identify strengths and weaknesses, and develop enterprise solutions comprising multiple capabilities. To address this recurring need in the near-term, we created D3FEND, a framework in which we encode a countermeasure knowledge base, but more specifically, a knowledge graph. The graph contains semantically rigorous types and relations that define both the key concepts in the cybersecurity countermeasure domain and the relations necessary to link those concepts to each other. We ground each of the concepts and relations to particular references in the cybersecurity literature. |
| NIS2 Directive (Directive on measures for a high common level of cybersecurity across the Union) | Directive (EU) 2022/2555 of the European Parliament and of the Council of 14 December 2022 on measures for a high common level of cybersecurity across the Union, amending Regulation (EU) No 910/2014 and Directive (EU) 2018/1972, and repealing Directive (EU) 2016/1148 (NIS 2 Directive). |
| NIST Cybersecurity Framework (CSF) | This publication is the result of an ongoing collaborative effort involving industry, academia, and government. The National Institute of Standards and Technology (NIST) launched the project by convening private- and public-sector organizations and individuals in 2013. Published in 2014 and revised during 2017 and 2018, this Framework for Improving Critical Infrastructure Cybersecurity has relied upon eight public workshops, multiple Requests for Comment or Information, and thousands of direct interactions with stakeholders from across all sectors of the United States along with many sectors from around the world. |
| NIST SP 800-53 (Security and Privacy Controls for Information Systems and Organizations) | A compliance policy providing a catalog of security and privacy controls for information systems and organizations to protect organizational operations and assets, individuals, other organizations, and the Nation from a diverse set of threats and risks, including hostile attacks, human errors, natural disasters, structural failures, foreign intelligence entities, and privacy risks. The controls are flexible and customizable and implemented as part of an organization-wide process to manage risk. The controls address diverse requirements derived from mission and business needs, laws, executive orders, directives, regulations, policies, standards, and guidelines. Finally, the consolidated control catalog addresses security and privacy from a functionality perspective (i.e., the strength of functions and mechanisms provided by the controls) and from an assurance perspective (i.e., the measure of confidence in the security or privacy capability provided by the controls). Addressing functionality and assurance helps to ensure that information technology products and the systems that rely on those products are sufficiently trustworthy. |
| PCI DSS (Payment Card Industry Data Security Standard) v4.0.0 | The Payment Card Industry Data Security Standard (PCI DSS) was developed to encourage and enhance payment card account data security and facilitate the broad adoption of consistent data security measures globally. PCI DSS provides a baseline of technical and operational requirements designed to protect account data. While specifically designed to focus on environments with payment card account data, PCI DSS can also be used to protect against threats and secure other elements in the payment ecosystem. |
| RBI Framework | Use of Information Technology by banks and their constituents has grown rapidly and is now an integral part of the operational strategies of banks. The Reserve Bank, had, provided guidelines on Information Security, Electronic Banking, Technology Risk Management and Cyber Frauds (G.Gopalakrishna Committee) vide Circular DBS.CO.ITC.BC.No.6/31.02.008/2010-11 dated April 29, 2011, wherein it was indicated that the measures suggested for implementation cannot be static and banks need to pro-actively create/fine-tune/modify their policies, procedures and technologies based on new developments and emerging concerns. |
| SEBI (Securities and Exchange Board of India) Act | An Act to provide for the establishment of a Board to protect the interests of investors in securities and to promote the development of, and to regulate, the securities market and for matters connected therewith or incidental thereto. |
| SOC 2 | SOC 2 is a voluntary compliance standard for service organizations, developed by the American Institute of CPAs (AICPA). Its intent is to ensure the safety and privacy of user data. It outlines the five trust service principles of security, availability, processing integrity, confidentiality, and privacy of customer data as a framework for safeguarding data. SOC 2 applies to any technology service provider or SaaS company that handles or stores customer data. Third-party vendors, other partners, or support organizations that those firms work with should also maintain SOC 2 compliance to ensure the integrity of their data systems and safeguards. |
{: caption="Available predefined policies" caption-side="top"}

All other posture policies apply to other environments such as AWS, Azure, GCP, Kubernetes, OpenShift, or hosts.

## List of Services Supported by {{site.data.keyword.sysdigsecure_short}}
{: #about-available-services}

{{site.data.keyword.sysdigsecure_full}} supports the following services for Cloud Security Posture Management (CPSM):

| Name of service |
|-----------------|
| [Cloud Object Storage](/docs/cloud-object-storage) |
| [Kubernetes Service](/docs/containers) |
| [Red Hat OpenShift](/docs/openshift) |
| [Virtual server for VPC](/docs/vpc?topic=vpc-creating-virtual-servers) |
| [Virtual Private Cloud](/docs/vpc) |
| [Block storage volume for VPC](/docs/vpc?topic=vpc-creating-block-storage) |
| [Block storage snapshots for VPC](/docs/vpc?topic=vpc-snapshots-vpc-create) |
| [Secrets Manager](/docs/secrets-manager) |
| [Databases for PostgreSQL](/docs/databases-for-postgresql) |
| [Databases for Redis](/docs/databases-for-redis) |
| [Databases for ElasticSearch](/docs/databases-for-elasticsearch) |
| [Databases for EnterpriseDB](/docs/databases-for-enterprisedb) |
| [Databases for ETCD](/docs/databases-for-etcd) |
| [Databases for MongoDB](/docs/databases-for-mongodb) |
| [Databases for MySQL](/docs/databases-for-mysql) |
| [Identity and Access Management](/docs/account?topic=account-cloudaccess) |
| [Key Protect](/docs/key-protect) |
| [Container Registry](/docs/Registry?topic=Registry-getting-started) |
| [Load Balancer for VPC](/docs/loadbalancer-service) |
| [Security Group for VPC](/docs/vpc?topic=vpc-using-security-groups) |
| [SSH Keys for VPC](/docs/vpc?topic=vpc-ssh-keys) |
| [Subnet for VPC](/docs/vpc?topic=vpc-about-subnets-vpc) |
| [Virtual Private Endpoint (VPE) for VPC](/docs/vpc?topic=vpc-ordering-endpoint-gateway&interface=ui) |
| [Auto Scale (Instance Group) for VPC](/docs/vpc?topic=vpc-creating-auto-scale-instance-group) |
| [Bare Metal servers for VPC](/docs/vpc?topic=vpc-planning-for-bare-metal-servers) |
| [Client VPN for VPC](/docs/vpc?topic=vpc-vpn-client-to-site-overview) |
| [Dedicated Host for VPC](/docs/vpc?topic=vpc-creating-dedicated-hosts-instances) |
| [Floating IP for VPC](/docs/vpc?topic=vpc-fip-about) |
| [Flow Logs](/docs/vpc?topic=vpc-flow-logs) - VPC |
| [Custom image for VPC](/docs/vpc?topic=vpc-planning-custom-images) |
| [Placement Groups for VPC](/docs/vpc?topic=vpc-about-placement-groups-for-vpc) |
| [Code Engine](/docs/codeengine) |
| [Network ACL - VPC](/docs/vpc?topic=vpc-using-acls) |
| [DNS Service - VPC](/docs/dns-svcs) |
| [VPN for VPC](/docs/vpc?topic=vpc-about-networking-for-vpc#external-connectivity) |
| [IBM Cloud Backup - VPC](/docs/vpc?topic=vpc-backup-service-about) |
| [Public Gateway](/docs/vpc?topic=vpc-vpn-create-gateway) |
| [Event Streams (messagehub)](/docs/EventStreams) |
| [IBM Cloud Direct Link](/docs/dl) |
| [Transit Gateway](/docs/transit-gateway) |
| [Toolchain](/docs/ContinuousDelivery) |
| [IBM Cloudant CLI](/docs/Cloudant-cli-plugin) |
| [IBM Cloud Internet Services (CIS)](/docs/cis) |
| [Schematics](/docs/schematics) |
| [Cloud Monitoring](/docs/monitoring?topic=monitoring-getting-started#getting-started)|
| [Security and Compliance Center (SCC)](/docs/security-compliance) |
| [Hyper Protect Crypto Services (HPCS)](/docs/hs-crypto) |
| [App ID](/docs/appid) |
| [App Configuration](/docs/app-configuration) |
| [Catalog Management](/docs/account?topic=account-restrict-by-user&interface=ui) |
| [Event Notifications](/docs/event-notifications) |
| [Messages for RabbitMQ](/docs/messages-for-rabbitmq) |
| [IBM Cloud Projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects) |
| [IBM Cloud Activity Tracker Event Routing](/docs/atracker) |
| [watsonx.ai Runtime](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/ml-overview.html?context=cpdaas) |
| [IBM Power Virtual Server](/docs/power-iaas) |
| [IBM Cloud Logs](/docs/cloud-logs) |
| [IBM Cloud Shell](/docs/cloud-shell?topic=cloud-shell-getting-started) |
{: caption="List of services supported by Workload Protection" caption-side="bottom"}

## Next steps
{: #about-next}

To get the most of {{site.data.keyword.sysdigsecure_short}} enable CSPM following the steps described in [Implementing CSPM (Cloud Security Posture Management) for {{site.data.keyword.cloud_notm}} using the UI and CLI](/docs/workload-protection?topic=workload-protection-cspm-implement).
