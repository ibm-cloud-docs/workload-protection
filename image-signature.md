---

copyright:
  years:  2025
lastupdated: "2025-11-17"

keywords:  supply chain, image signature

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Image Signature validation
{: #image-signature-validation}

The Image Signature validation policy enforces that only container images signed by trusted sources are admitted into Kubernetes and OpenShift Clusters. This prevents the use of unsigned or tampered images in your workloads. 

The Image Signature validation is powered by [Cosign](https://docs.sigstore.dev/cosign/verifying/verify/).

## Limitations
{: #image-signature-validation-limitatoins}

- Container Workloads scanned agentlessly are not supported.
- Runtime Container Workloads post-admission are not yet supported.
- Registry-level enforcement and attestations are not yet supported.
- CLI-level enforcement and attestations are not yet supported.

## Admission Control stage
{: #image-signature-validation-capabilities-admission-stage}

An Admission Control stage and scope is specifically used with the Admission Controller in Cluster Shield. This stage supports the following filtering in an `AND` fashion and can be used to `Warn` or `Reject` images that fail the policy checks. It is the only Vulnerability Management Policy with a `Warning` function.

* **Scopes:**
  * **Kubernetes Labels:** `kubernetes.cluster.distribution`, `kubernetes.cluster.name`, `kubernetes.namespace.name`, `kubernetes.node.name`, `kubernetes.pod.container.name`, `kubernetes.workload.name`, `kubernetes.workload.type`
  * **Supported Operators:**  `is`: Single Value, `is not`: Single Value, `in`: Single Value or List, `not in`: Single Value or List, `contains`: Single Value, `not contains`: Single Value, `starts with`: Single Value
  * **Image Reference:** The pullstring of the image you wish to target for the specific Registry or Repository
    * **Supported Operators:** `starts with`: Single Value, `is`: Single Value, `is not`: Single Value, `contains`: Single Value, `not contains`: Single Value

Image Signature validation in the Admission Controller is available starting with Cluster Shield 1.17.0
{:note}

## Example use cases
{: #image-signature-validation-capabilities-examples}

- Enforce that all production workloads use images signed by your CI/CD pipeline.
- Prevent unsigned third-party images from being deployed.  
- Align with compliance frameworks requiring artifact signature validation.  

## Integration Guides
{: #image-signature-validation-integrations}

The Image Signature Validation Policy can integrate with multiple signing and verification sources depending on your organization’s environment and trust model.

Refer to the following guides for setup instructions specific to each integration type:

| Integration Type | Description | Link |
|------------------|--------------|------|
| **Red Hat Trusted Artifact Signer (RHTAS)** | Use a Red Hat–supported Sigstore deployment to verify images signed within Red Hat or OpenShift environments. | [How to Integrate with RHTAS](/docs/workload-protection?topic=workload-protection-image-signature-validation-rhtas) |
| **GitHub and Sigstore** | Verify images signed by GitHub Actions workflows using Sigstore’s public Fulcio and Rekor services. | [How to Integrate with GitHub + Sigstore](https://docs.sysdig.com/en/docs/sysdig-secure/policies/supply_chain_policies/how-to-github-sigstore) |
| **Self-hosted Sigstore** | Integrate with your organization’s private Sigstore stack (Fulcio, Rekor, and TUF) for internal OIDC or key-based signing. | [How to Integrate with a self-hosted Sigstore](https://docs.sysdig.com/en/docs/sysdig-secure/policies/supply_chain_policies/how-to-self-hosted-sigstore) |

{{site.data.keyword.sysdigsecure_short}} supports verification through any standard [Cosign](https://docs.sigstore.dev/cosign/verifying/verify/) mechanism as long as `cosign verify` is compatible with your signing configuration and `cosign verify` is [compatible with that issuer](https://docs.sigstore.dev/certificate_authority/oidc-in-fulcio/#supported-oidc-token-issuers).
{:note}

## Signature Caching
{: #image-signature-validation-caching}

The **Admission Controller** uses a **15-minute cache** to reduce registry overhead when validating image signatures.

During this period, any change to an image’s signature in the registry is not immediately reflected.

Deployments will continue to be allowed or rejected based on the cached signature state until the cache refreshes.

Using digest-pinned image references and understanding the 15-minute cache behavior ensures predictable validation, consistent security posture, and reliable deployments across environments.

---

### Considerations when using the image signature validation feature
{: #image-signature-validation-scenario-impacts}

| Scenario                                      | Description                                                                          | Impact                                                                                                                                                                  |
| --------------------------------------------- | ------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Signature added or changed in registry** | An image without a valid signature is updated with a valid one while still cached.   | The Admission Controller continues to treat the image as unsigned until the 15-minute cache expires.                                                                    |
| **2. Mutable tags used in deployments**       | Deployments use mutable tags like `latest`, `1`, or `dev` that can change over time. | Cached validations may not match the actual image content, potentially leading to inconsistent admission decisions. Mutable tags are not recommended in Kubernetes. |
