---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Scanning Kubernetes containers
{: #scan_kube}

{{site.data.keyword.mon_full}} provides controls to evaluate the configuration of container runtimes (for example, Docker) using Posture capabilities. These controls include host configuration and running container configuration. Scanning detects running containers, vulnerabilities in those containers, incorrect configurations, passwords in plain text in any file or variable.
{: shortdesc}

You must be assigned the administrator role to run these steps.
{: note}

## Configuring Kubernetes container monitoring
{: #config_kube_scan}

To configure container monitoring you need to:

1. Configure a compliance posture and scanning.

2. Install and configure admission controllers on your clusters.

2. Configure Admission Controller rules to stop deployment of images with vulnerabilties.

3. Enable runtime policies.

## Configuring a compliance posture and scanning
{: #conf_posture}

1. Launch the [{{site.data.keyword.mon_short}} Secure console](/docs/monitoring?topic=monitoring-launch#launch_step3).

2. Hover over **Posture**.

3. Click **New Report**.

4. Click the appropriate benchmark for your container. For example, **Docker Security Benchmark**.

5. Configure your scanning report and the schedule when the scanning is run.

    ![Panel showing the report details configuration.](images/sec_report_details.png "Configuring report details"){: caption="Figure 1. Configuring report details" caption-side="bottom"}

    * For **Report Name** specify a unique name for your report.

    * For **Framework** select the scanning you want run.

    * For **Version** select the version of the **Framework** to run.

    * For **Platform** select the platform to scan.

    * For **Scope** select if you want to limit the scope of the scan. By default the entire infrastructure is scanned.

    * For **Schedule** indicate when you want the scan to run.

    * If you want all framework items scanned and included in the report, enable the **All Sections** switch. If you want to limit the scanning to only specific areas, disable the **All Sections** switch and and select the checkboxes for the sections you want scanned.

        ![Panel showing report limited to 1.1 sections only.](images/sec_report_details_2.png "Configuring report to include only specfic sections"){: caption="Figure 2. Configuring report to include only specfic sections" caption-side="bottom"}

6. Click **Schedule Report**.

Your report is displayed in the list and is enabled by default. To disable a report, click the enable switch to disable.

## Installing the admission controller
{: #inst_admin_ctl}

The [admission controller](https://docs.sysdig.com/en/docs/sysdig-secure/scanning/admission-controller/#admission-controller){: external} defines and customizes requests allowed on a cluster. The controller needs to be on all clusters that are monitored.

1. Make sure `kubectl` is pointing to the target cluster where you want to install the admission controller and Helm version 3 or greater is installed.

2. Run the following commands to access the Helm repository:

   ```sh
   helm repo add sysdig https://charts.sysdig.com
   helm repo update
   ```
   {: codeblock}

3. Use `sysdig-deploy` to deploy the latest helm chart:

   ```sh
   helm install sysdig sysdig/sysdig-deploy \
       --set global.sysdig.accessKey=ACCESS_KEY \
       --set global.sysdig.secureAPIToken=SECURE_API_TOKEN \
       --set global.clusterConfig.name=CLUSTER_NAME \
       --set admissionController.enabled=true \
       --set admissionController.sysdig.url=SECURE_URL
   ```
   {: codeblock}

## Creating admission controller policies
{: #conf_admin_cont_policy}

Create policies defining when to accept or reject a container image at admission time.

Policies must be assigned to a cluster to be enforced.
{: important}

1. Launch the [{{site.data.keyword.mon_short}} Secure console](/docs/monitoring?topic=monitoring-launch#launch_step3).

2. Hover over **Scanning**.

3. Click **Admission Controller** > **Policies**.

4. Click **Create a new policy**.

5. Configure your admission controller policy.

   ![Panel defining an admission controller policy.](images/sec_admin_policy.png "Configuring an admission controller policy"){: caption="Figure 3. Configuring an admission controller policy" caption-side="bottom"}

   * For **Name** specify a name for your policy.

   * For **Description** give a description of your policy.

   * For **Evaluation Fail** specify if the image is rejected (`reject`) when the scanning policy fails. Images assigned to a policy without scan results will also be reject. Specifying `ignore` bypasses this check.

   * For **Evaluation Age** specify if the image is rejected (`reject`) when the scan is older than the specified number of days. Specifying `ignore` bypasses this check.

   * For **Unscanned Image** specify one of the following:

     `Ignore`
     :   This condition is bypassed and unscanned images are admitted.

     `Reject`
     :   Unscanned images are rejected.

     `Reject and Scan`
     :   Unscanned images are rejected and an image scan started.

   * Click **Save**.

## Assigning admission controller policies
{: #config_run_policies}

You will not be able to assign policies until you have [containers with admission controllers installed](#config_kube_scan) and [admission controller policies defined.](#conf_admin_cont_policy)
{: important}

1. Launch the [{{site.data.keyword.mon_short}} Secure console](/docs/monitoring?topic=monitoring-launch#launch_step3).

2. Hover over **Scanning**.

3. Click **Admission Controller** > **Policies Assignments**. The list of Kubernetes clusters with admission controllers and their status is displayed.

   Clusters where the admission admission controller was never installed will not be listed.
   {: note}

   Status is one of the following:

   `Connected`
   :   The admission controller associated with the cluster is connected and healthy.

   `Disconnected`
   :   The admission controller is installed on the cluster but is not reporting to {{site.data.keyword.mon_full_notm}}.

4. Click the cluster you want to configure.

4. Enable or disable the admission controllers on the desired clusters by selecting the appropriate switch.

   `Enabled`
   :   The admission controller is enabled and the associated policies are enforced.

   `Disabled`
   :   The admission controller is disabled.

4. Click **Add Assignment** to add assignment details. A cluster can have multiple assignments. Policies are evaluated from top to bottom of the list.

   `Namespace`
   :   Leave blank to match any namespace or add a regular expression to match a namespace. For example:

       `dev`
       :   Match any namespace containing the string `dev`.

       `^dev`
       :   Match any namespace beginning with the string `dev`.

       `^dev$`
       :   Matches only a namespace with the exact name `dev`.

    `Prefix`
    :   Leave blank to match any image name or limit by entering a prefix. For example, `redis` would match images declared as `redis:latest` or `redis:v2` in the container creation request.

    `Policy`
    :   Select a [policy](#conf_admin_cont_policy) to associate with the cluster.

5. For **Default policy if no other assignment matches**  select `allow` to allow images to be run or `reject` to reject images that do not match any defined policy.

   Be careful when using the `reject` option. When specifying `reject` as the default make sure you have explicit policies allowing critical workloads.
   {: attention}
