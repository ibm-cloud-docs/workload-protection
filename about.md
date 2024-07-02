---

copyright:
  years:  2023, 2024
lastupdated: "2024-07-02"

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

## Next steps
{: #about-next}

To get the most of {{site.data.keyword.sysdigsecure_short}} enable CSPM following the steps described in [Implementing CSPM (Cloud Security Posture Management) for {{site.data.keyword.cloud_notm}} using the UI and CLI](/docs/workload-protection?topic=workload-protection-cspm-implement).