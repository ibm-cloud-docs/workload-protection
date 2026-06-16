---

copyright:
  years:  2026
lastupdated: "2026-06-16"

keywords: cloud detection and response, CDR, ibm cloud

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my {{site.data.keyword.cloud_notm}} account not ingesting audit events
{: #ts-cdr}
{: troubleshoot}

After enabling CDR for your {{site.data.keyword.cloud_notm}} account, the account does not appear as `Connected` under Integrations > Environments > {{site.data.keyword.cloud_notm}} in your {{site.data.keyword.sysdigsecure_short}} instance.
{: tsSymptoms}

The CDR connection might not be active for one of the following reasons:
{: tsCauses}

- The Trusted Profile was not created correctly, or the {{site.data.keyword.sysdigsecure_short}} instance CRN is not set as a trusted entity in the profile.
- The Trusted Profile does not have the required IAM access policies to read from the {{site.data.keyword.cos_short}} bucket or view the Service ID.
- The {{site.data.keyword.atracker_short}} target is not writing to the {{site.data.keyword.cos_short}} bucket correctly.
- The {{site.data.keyword.codeengineshort}} application is not running, either because the registry secret is missing or the API key is incorrect.
- The IAM service-to-service authorization policy between {{site.data.keyword.codeengineshort}} and {{site.data.keyword.cos_full_notm}} is missing, preventing {{site.data.keyword.cos_short}} event notifications from being delivered.
- The {{site.data.keyword.cos_short}} event subscription destination does not match the {{site.data.keyword.codeengineshort}} application name.
- The parameters in step 7 (`cdr_bucket_region`, `cdr_bucket_name`, `cdr_ingestion_url`) do not match the resources created in previous steps.

To resolve this issue, complete the following steps:
{: tsResolve}

1. Verify that the {{site.data.keyword.atracker_short}} target is writing successfully to the {{site.data.keyword.cos_short}} bucket:

   ```sh
   ibmcloud atracker target get --target <target_name>
   ```
   {: pre}

   Check that `Write Status` shows `success`. If it shows an error, verify that the service-to-service authorization between {{site.data.keyword.atracker_short}} and {{site.data.keyword.cos_full_notm}} is enabled and that the bucket exists in the expected region.

2. Confirm that the Trusted Profile includes the {{site.data.keyword.sysdigsecure_short}} instance CRN as a trusted entity and has the required access policies:

   ```sh
   ibmcloud iam trusted-profile-get ibmcdr-wp-cos
   ```
   {: pre}

   Ensure the trust relationship points to the correct {{site.data.keyword.sysdigsecure_short}} CRN and that policies for `cloud-object-storage` (Viewer, Reader on the bucket) and `iam-identity` (Viewer on the Service ID) are present.

3. Check that the {{site.data.keyword.codeengineshort}} application is running:

   ```sh
   ibmcloud ce application get --name sccwp-cdr-app
   ```
   {: pre}

   If the application is not ready, verify that the `icr-secret` registry secret is correctly configured and that the `cdr-secrets` secret contains a valid API key. If the image cannot be pulled, confirm that the Service ID has Reader access to the {{site.data.keyword.registrylong_notm}}.

4. Verify that the IAM authorization policy between {{site.data.keyword.codeengineshort}} and {{site.data.keyword.cos_full_notm}} exists:

   ```sh
   ibmcloud iam authorization-policies
   ```
   {: pre}

   Look for a policy granting {{site.data.keyword.codeengineshort}} the `Notifications Manager` role on the {{site.data.keyword.cos_full_notm}} instance. If missing, rerun the authorization policy command from step 6 of the setup.

5. Check that the {{site.data.keyword.cos_short}} event subscription is ready and pointing to the correct application:

   ```sh
   ibmcloud ce subscription cos get --name cdr-cos-sub
   ```
   {: pre}

   Confirm that `Destination` matches `sccwp-cdr-app`, `Bucket` matches your {{site.data.keyword.cos_short}} bucket name, and `Ready` shows `true`.

6. Verify that the {{site.data.keyword.sysdigsecure_short}} instance was updated with the correct parameters by re-running step 7 of the setup with the correct values. Ensure that `cdr_bucket_region`, `cdr_bucket_name`, `cdr_trusted_profile_id`, `cdr_service_id`, and `cdr_ingestion_url` all match the resources created in previous steps.

7. After making any corrections, allow up to 5 minutes for the connection status to update in the {{site.data.keyword.sysdigsecure_short}} UI.

For more information, see [Enabling Detection and Response for {{site.data.keyword.cloud_notm}}](/docs/workload-protection?topic=workload-protection-cdr-tutorial).
