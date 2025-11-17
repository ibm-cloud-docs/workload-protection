---

copyright:
  years:  2025
lastupdated: "2025-11-17"

keywords:  supply chain, image signature

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Supply chain policies
{: #supply-chain-policies}

{{site.data.keyword.sysdigsecure_short}} **supply chain policies** help you validate the trust and integrity of software artifacts before they are deployed into your Kubernetes or OpenShift environments.

These policies are designed to help you verify that artifacts such as container images, SBOMs, and other workload components:

- Originate from trusted build systems or registries. 
- Have not been modified after publication.
- Comply with organizational and regulatory requirements for software provenance and integrity.

Supply chain policies goals:
| Objective        | Description                                                                                               |
| ---------------- | --------------------------------------------------------------------------------------------------------- |
| **Integrity**    | Validate that images and artifacts have not been altered from their intended state.                       |
| **Authenticity** | Ensure that artifacts are signed by trusted publishers, CI/CD systems, or registries.                     |
| **Compliance**   | Enforce adherence to enterprise and regulatory requirements for software provenance and chain-of-custody. |


## Prerequisites
{: #supply-chain-policies-prerequisites}

Before enabling supply chain policies, ensure that {{site.data.keyword.sysdigsecure_short}} components are installed on your Kubernetes clusters. 

- See [Managing the agent in a Kubernetes cluster by using Helm](/docs/workload-protection?topic=workload-protection-agent-deploy-kube-helm) for deployment instructions.  
- Verify that the **supply_chain** feature is enabled in your cluster shield configuration.

```yaml
features:
  supply_chain:
    enabled: true
```

## Supported Policy Types
{: #supply-chain-policies-supported-policies}

The following policy type is supported:

### [**Image Signature Validation**](/docs/workload-protection?topic=workload-protection-image-signature-validation)
{: #supply-chain-policies-supported-policies-image-signature-validation}

The Image Signature Validation policy enforces that only container images with valid digital signatures are admitted into your Kubernetes and OpenShift clusters.
Signatures can be verified through:

* **Public Key** validation (using PEM-encoded public keys).
* **OIDC Provider** validation (e.g., GitHub Actions, Red Hat Trusted Artifact Signer, Google, AWS STS, Microsoft Entra ID, or any compatible Sigstore implementation).

This policy operates at the Admission Control stage.
It prevents unsigned or tampered images from being deployed, ensuring supply chain integrity before workloads are scheduled to run.
