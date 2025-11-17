---

copyright:
  years:  2025
lastupdated: "2025-11-17"

keywords:  supply chain, image signature

subcollection: workload-protection

---

# Image Signature validation with Red Hat Trusted Artifact Signer (RHTAS)
{: #image-signature-validation-rhtas}

The **Red Hat Trusted Artifact Signer (RHTAS)** provides an enterprise-grade, Red Hat-supported implementation of the [Sigstore](https://www.sigstore.dev) project for securely signing and verifying container images and other software artifacts.

When integrated with Kubernetes or OpenShift admission control, RHTAS enables organizations to enforce signature verification policies that ensure only trusted and verifiable images are admitted to clusters.

RHTAS includes the full Sigstore stack:

- **Fulcio**: issues short-lived, OIDC-based signing certificates.  
- **Rekor**: records immutable transparency logs of signing events.  
- **TUF**: distributes and manages trust roots for verification.  

Together, these components create a verifiable chain of trust that prevents tampering, strengthens supply chain integrity, and simplifies compliance for signed artifacts.

For more information, see the [Red Hat Trusted Artifact Signer](https://docs.redhat.com/en/documentation/red_hat_trusted_artifact_signer).

## Purpose of Admission Control Integration
{: #image-signature-validation-rhtas-admissioncontroller}

Integrating RHTAS with {{site.data.keyword.sysdigsecure_short}} allows Kubernetes and OpenShift administrators to enforce admission-time verification of container images.  

This ensures that only signatures issued by your RHTAS instance and by your organization’s trusted identities are accepted.

During deployment, {{site.data.keyword.sysdigsecure_short}} verifies each image against the configured RHTAS trust root and OIDC identity to ensure that:

- Only verified images signed through RHTAS are admitted to the cluster.  
- Supply chain integrity is maintained from build to production.  
- Tampering and substitution attacks are blocked before execution.  
- Compliance frameworks (for example, SLSA or NIST 800-204D) are supported through transparent verification and logging.

### Benefits
{: #image-signature-validation-rhtas-benefits}

Integrating RHTAS with {{site.data.keyword.sysdigsecure_short}} Admission Controller in Cluster Shield extends software supply chain trust directly into Kubernetes and OpenShift admission control.  

This ensures that only authentic, verifiable container images signed by your RHTAS instance are deployed. It strengthens runtime security and maintains a provable chain of custody from build to production.

| Capability | Description |
|-------------|-------------|
| **Policy-driven enforcement** | Integrates with {{site.data.keyword.sysdigsecure_short}} Admission Control to automatically reject unsigned or invalid images. |
| **Identity-based verification** | Uses Fulcio-issued short-lived certificates tied to developer or system OIDC identities. |
| **Immutable transparency logs** | Rekor maintains tamper-evident logs for all signing events. |
| **Consistent trust model** | Applies the same RHTAS trust root across build, registry, and runtime environments. |
| **Operational simplicity** | Red Hat manages and supports the Sigstore components, reducing PKI complexity. |


## Configuration
{: #image-signature-validation-rhtas-configuration}

You need to configure the Cluster Shield and the Policy to enable verification against your RHTAS instance.

### Configuring Cluster Shield
{: #image-signature-validation-rhtas-configuration-cluster-shield}

To enable verification against your RHTAS instance, configure [Cluster Shield](/docs/workload-protection?topic=workload-protection-agent-deploy-kube-helm) with your RHTAS trust root details. 

Cluster Shield performs runtime verification using the TUF root and checksum you provide.

You need the following from your RHTAS deployment:

1. **RHTAS hostname** (for example: `rhtas.apps.acme-cluster.example.com`)  
2. **TUF root file URL** (for example: `https://tuf.rhtas.apps.acme-cluster.example.com/root.json`)  
3. **TUF root checksum** (SHA-256 or SHA-512 format)

Using the [{{site.data.keyword.sysdigsecure_short}} Helm chart](/docs/workload-protection?topic=workload-protection-agent-deploy-kube-helm), configure the following parameters:

```yaml
features:
  supply_chain:
    enabled: true
    image_signature:
      cosign:
        mirror: https://tuf.rhtas.apps.acme-cluster.example.com
        # Optional: only override if your root differs from the default RHTAS location
        root: https://tuf.rhtas.apps.acme-cluster.example.com/example/root.json
        root_checksum: sha256:8d31cb9e6b5f89c224e621e1eac5e4d3bcd20a02e31d69394f0f8b62f88e743c
```

### Policy Configuration
{: #image-signature-validation-rhtas-configuration-policy}

All trust and identity settings for signature verification are defined in the {{site.data.keyword.sysdigsecure_short}} backend [Image Signature Validation Policy](/docs/workload-protection?topic=workload-protection-image-signature-validation).

To validate signatures created by RHTAS, configure your policy using the OIDC Provider (validation type) mechanism under **Policies / Supply Chain / Policies**:

1. Set the **OIDC Issuer** to match your RHTAS Fulcio issuer endpoint (for example, `https://keycloak.rhtas.apps.acme-cluster.example.com/realms/trusted-artifacts`).
2. Define the **Certificate Identity** corresponding to the signing user, service account, or build system (regex supported).
3. Optionally provide a **Certificate Chain** in PEM format to override the default TUF-rooted trust chain used by Cluster Shield.

The following is an example with the required configuration in the policy to integrate with RHTAS:

| Field  | Example Value    | Description       |
| ------ | ---------------- | ----------------- |
| **OIDC Issuer** | `^https://keycloak.rhtas.apps.acme-cluster.example.com/realms/trusted-artifacts$`| OIDC issuer used by your RHTAS Fulcio instance.|
| **Certificate Identity** | `^system:serviceaccount:ci-pipeline:signer$`| Identity pattern for the signer.|
| **Certificate Chain (optional)** | PEM-encoded chain of intermediate and root certs.| Used to override the default trust chain if required. |

The following is an example of a certificate chain in PEM Format.

```text
-----BEGIN CERTIFICATE-----
MIIGczCCBJegAwIBAgIQDk... (Server Certificate)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIF7jCCA9mgAwIBAgIQ... (Intermediate Certificate)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIF7jCCA9mgAwIBAgIQ... (Root Certificate)
-----END CERTIFICATE-----
```
