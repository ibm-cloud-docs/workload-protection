---

copyright:
  years:  2023, 2024
lastupdated: "2024-07-11"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# About IBM Cloud Security Posture Management (CSPM)
{: #about}

In {{site.data.keyword.cloud_notm}}, {{site.data.keyword.sysdigsecure_full}} automates compliance checks for [{{site.data.keyword.cloud_notm}} Framework for Financial Services](/docs/framework-financial-services?topic=framework-financial-services-about), Digital Operational Resilience Act (DORA), CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark, PCI and many other industrial related or best practices standards. With a detailed inventory of your {{site.data.keyword.cloud_notm}} resources and prioritization based on full context it facilitates the resolution and management of collected violations.

The {{site.data.keyword.sysdigsecure_short}} posture module supports compliance validation on {{site.data.keyword.cloud_notm}}, multi-cloud environments (Amazon Web Services, Azure and Google Cloud), inside hosts, virtual machines (VSIs for VPC, VMware, PowerVS and IBM Z with Linux), Kubernetes, and OpenShift.
{: note}

The posture module brings many features for your CSPM in your hybrid environments:

- Unified and centralized view to manage security and compliance of applications, workloads and infrastructure running on {{site.data.keyword.cloud_notm}}, in other cloud providers and on-premise, covering managed services, hosts, virtual machines and containers and Kubernetes or OpenShift clusters.

- Docens of predefined frameworks such as Financial Services, PCI, DORA, CIS or NIST allow to implement and validate the controls that are required to meet industry standards and laws.

- Inventory of all your cloud assests (compute resources, managed services, identities, and entitlements) and hosts, virtual machines, clusters and all Kubernetes or OpenShift resources, whether they are in the cloud or on-premises.

- A risk acceptance flow for removing the violation from the failed controls with options for the reason and expiration period for the acceptance. Risk can be accepted at one resource level or globally for all resources from one control.

- Detailed remediation instructions to fix failing controls.

## Available pre-defined policies for IBM Cloud CSPM in {{site.data.keyword.sysdigsecure_short}}

The following posture policies are available for you to use to implement CSPM for your {{site.data.keyword.cloud_notm}} resources:

| Policy  | Description |
|:---------|:------------|
| CIS {{site.data.keyword.cloud_notm}} Foundations Benchmark | Validate that your resource configurations meet the baseline requirements that are identified by the Center for Internet Security. |
| {{site.data.keyword.cloud_notm}} Framework for Financial Services | [{{site.data.keyword.cloud_notm}} for Financial Services™](/docs/framework-financial-services?topic=framework-financial-services-about) is an open platform that brings together independent software vendors (ISVs), Software as a Service (SaaS) providers, and financial services institutions in a single ecosystem. In this secure cloud platform, you can rapidly develop and share innovative applications, APIs, data, and content to meet the unique business needs of your financial institution.  \n \n Through the [{{site.data.keyword.framework-fs_full}}](/docs/framework-financial-services?topic=framework-financial-services-about), you can access a unified set of security and compliance controls, which was built specifically for and with the financial services industry. To address your evolving needs as a financial institution, IBM continuously validates these controls with global Councils of CSOs, CTOs, and CIOs from major banks, insurance providers, and regulatory advisors.  \n \n The {{site.data.keyword.cloud_notm}} for Financial Services profile provides you with a set of pre-configured automated goals that are mapped to the [{{site.data.keyword.framework-fs_full}} control requirements](/docs/framework-financial-services?topic=framework-financial-services-about#framework-control-requirements). The results of these tests help you validate compliance when you are using one of the [references architectures](/docs/framework-financial-services?topic=framework-financial-services-reference-architecture-overview) for the {{site.data.keyword.cloud_notm}} for Financial Services. |
{: caption="Table 2. Available predefined policies" caption-side="top"}

All other posture policies apply to other environments such as AWS, Azure, GCP, Kubernetes, OpenShift, or hosts.

## Next steps
{: #about-next}

To get the most of {{site.data.keyword.sysdigsecure_short}} enable CSPM following the steps described in [Implementing CSPM (Cloud Security Posture Management) for {{site.data.keyword.cloud_notm}} using the UI and CLI](/docs/workload-protection?topic=workload-protection-cspm-implement).