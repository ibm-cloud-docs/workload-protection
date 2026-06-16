---

copyright:
  years:  2023, 2026
lastupdated: "2026-06-16"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent in {{site.data.keyword.redhat_openshift_notm}} by using a Helm chart
{: #agent-deploy-openshift-helm}

You can use a Helm chart to install, upgrade, and delete a {{site.data.keyword.sysdigsecure_short}} agent on a {{site.data.keyword.redhat_openshift_notm}} cluster.
{: shortdesc}

You can also use the console to connect an existing {{site.data.keyword.redhat_openshift_notm}} or Kubernetes cluster to your instance of {{site.data.keyword.sysdigsecure_short}}. In the {{site.data.keyword.cloud_notm}} console, go to **Containers > Clusters** to access the existing cluster. Then, click **Connect** in the {{site.data.keyword.sysdigsecure_short}} widget to connect your cluster to {{site.data.keyword.sysdigsecure_short}}.
{: fast-path}

## Before you begin
{: #agent-deploy-openshift-helm-prereqs}

- Install the latest release of the [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine. Helm version 3.6 or later is required. 
- Install the {{site.data.keyword.cloud_notm}} CLI, the {{site.data.keyword.containershort_notm}} plug-in, the {{site.data.keyword.registrylong_notm}} plug-in, and the {{site.data.keyword.redhat_openshift_notm}} and Kubernetes CLIs. For more information, go to [Installing the CLI](/docs/openshift?topic=openshift-cli-install).
- Verify that you have the required access and permissions to deploy the {{site.data.keyword.sysdigsecure_short}} agent on the cluster.
- Verify that the `ibm-observe` project is available in your cluster. The agent is deployed in this project.

    A project is a namespace in a cluster.

    To create the project, run `oc adm new-project --node-selector='' ibm-observe`.
    {: tip}

- Verify that outbound traffic from your cluster to {{site.data.keyword.sysdigsecure_short}} endpoints is allowed on ports `443` and `6443`. If you connect the agents through a Virtual Private Endpoint (VPE), both ports must be allowed for outbound traffic from the cluster.

## Deploying an agent
{: #agent-deploy-openshift-helm-deploy}

Complete the following steps to deploy an agent by using Helm.

### Set up the cluster context
{: #agent-deploy-openshift-helm-install-step1}

1. Log in to your account. If you have a federated account, include the `--sso` option.

    ```sh
    ibmcloud login [-g <resource_group>] [--sso]
    ```
    {: pre}

2. Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable.

    ```sh
    ibmcloud oc cluster config --cluster <cluster_name_or_ID>
    ```
    {: pre}

3. In your browser, navigate to the address of your cluster controller URL and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.

4. From the {{site.data.keyword.redhat_openshift_notm}} web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate from the CLI.

5. Verify that the `oc` commands run properly with your cluster by checking the version.

    ```sh
    oc version
    ```
    {: pre}

    Example output:

    ```sh
    Client Version: v4.11.0
    Kubernetes Version: v1.25.8.2
    ```
    {: screen}

    If you can't perform operations that require Administrator permissions, such as listing all the worker nodes or pods in a cluster, download the TLS certificates and permission files for the cluster administrator by running the `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` command.
    {: tip}

### Set up the Sysdig Helm repository
{: #agent-deploy-openshift-helm-install-step2}

Add the {{site.data.keyword.sysdigsecure_short}} Helm repository to your Helm instance.

1. Add the Helm repository.

    ```sh
    helm repo add sysdig https://charts.sysdig.com
    ```
    {: pre}

2. Update the repository to retrieve the latest versions of all Helm charts.

    ```sh
    helm repo update
    ```
    {: pre}

3. List the Helm charts that are currently available for the Sysdig repository.

    ```sh
    helm search repo sysdig
    ```
    {: pre}

4. Verify that the `sysdig/sysdig-deploy` Helm chart is listed.

### Create the values `YAML` file
{: #agent-deploy-openshift-helm-install-step3}

Define a `YAML` file and include the values to deploy the {{site.data.keyword.sysdigsecure_short}} agent and the Secure components that you plan to deploy. For example, name the file `agent-values-monitor-secure.yaml`.

The following `YAML` is a template that you can use to configure the {{site.data.keyword.sysdigsecure_short}} agent and the Secure components. You can customize the file by removing or commenting with `#` the sections that are not required for your agent.

```yaml
agent:
  ebpf:
    enabled: true
    kind: universal_ebpf
  collectorSettings:
    collectorHost: INGESTION_ENDPOINT
  sysdig:
    settings:
      host_scanner:
        enabled: true
      kspm_analyzer:
        enabled: true
      sysdig_api_endpoint: API_ENDPOINT
  extraVolumes:
    volumes:
    - name: root-vol
      hostPath:
        path: /
    - name: tmp-vol
      hostPath:
        path: /tmp
    mounts:
    - mountPath: /host
      name: root-vol
      readOnly: true
    - mountPath: /host/tmp
      name: tmp-vol
global:
  imageRegistry: icr.io/ext
  clusterConfig:
    name: CLUSTER_NAME
  sysdig:
    accessKey: SERVICE_ACCESS_KEY
    apiHost: API_ENDPOINT
nodeAnalyzer:
  enabled: false
clusterShield:
  enabled: true
  cluster_shield:
    sysdig_endpoint:
      region: custom
      collector: INGESTION_ENDPOINT:6443
    log_level: info
    features:
      admission_control:
        enabled: true
        container_vulnerability_management:
          enabled: true
        dry_run: false
      container_vulnerability_management:
        enabled: true
      audit:
        enabled: true
      posture:
        enabled: true
```
{: codeblock}

Where:

`CLUSTER_NAME`
:   The name of the cluster where you are deploying the agent.

`SERVICE_ACCESS_KEY`
:   The {{site.data.keyword.sysdigsecure_short}} instance access key.

`INGESTION_ENDPOINT`
:   The instance's ingestion endpoint. For example, `ingest.us-east.security-compliance-secure.cloud.ibm.com`.

`API_ENDPOINT`
:   The instance's API endpoint. For example, `us-east.security-compliance-secure.cloud.ibm.com`.

### Install the Helm chart
{: #agent-deploy-openshift-helm-install-step4}

To deploy the agent, the Secure components, or both, install the `sysdig/sysdig-deploy` chart and use the variables `YAML` file that you configured in the previous step.

Run the following command to install the agent by using the Helm chart:

```sh
helm install -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
```
{: pre}

The following example shows a sample Helm values file for the `us-east` region:

```yaml
agent:
  ebpf:
    enabled: true
    kind: universal_ebpf
  collectorSettings:
    collectorHost: ingest.private.us-east.security-compliance-secure.cloud.ibm.com
  sysdig:
    settings:
      host_scanner:
        enabled: true
      kspm_analyzer:
        enabled: true
      sysdig_api_endpoint: private.us-east.security-compliance-secure.cloud.ibm.com
  extraVolumes:
    volumes:
    - name: root-vol
      hostPath:
        path: /
    - name: tmp-vol
      hostPath:
        path: /tmp
    mounts:
    - mountPath: /host
      name: root-vol
      readOnly: true
    - mountPath: /host/tmp
      name: tmp-vol
global:
  imageRegistry: icr.io/ext
  clusterConfig:
    name: my-cluster
  sysdig:
    accessKey: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx
    apiHost: private.us-east.security-compliance-secure.cloud.ibm.com
nodeAnalyzer:
  enabled: false
clusterShield:
  enabled: true
  cluster_shield:
    sysdig_endpoint:
      region: custom
      collector: ingest.private.us-east.security-compliance-secure.cloud.ibm.com:6443
    log_level: info
    features:
      admission_control:
        enabled: true
        container_vulnerability_management:
          enabled: true
        dry_run: false
      container_vulnerability_management:
        enabled: true
      audit:
        enabled: true
      posture:
        enabled: true
```
{: codeblock}

## Updating an agent
{: #agent-deploy-openshift-helm-update}

To update the agent version by using Helm, complete the following steps:

1. Update the Helm repository.

    ```sh
    helm repo update
    ```
    {: pre}

2. Upgrade the agent.

    ```sh
    helm upgrade -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
    ```
    {: pre}

These steps upgrade your agents to the latest available version.

## Removing an agent
{: #agent-deploy-openshift-helm-delete}

You can also use the console to remove the agent from your cluster. In the {{site.data.keyword.cloud_notm}} console, go to **Containers > Clusters** to access the existing cluster. Then, open the **Options** menu in the {{site.data.keyword.sysdigsecure_short}} widget and select **Disconnect**.
{: fast-path}

To delete the agent by using Helm, uninstall the chart.

1. List the charts that are installed.

    ```sh
    helm list -n ibm-observe
    ```
    {: pre}

    The output lists the installed charts:

    ```text
    NAME        	NAMESPACE  	REVISION	UPDATED                             	STATUS  	CHART              	APP VERSION
    sysdig-agent	ibm-observe	1       	2023-03-24 15:02:58.408108 +0100 CET	deployed	sysdig-deploy-1.6.3
    ```
    {: screen}

2. Uninstall the chart.

    ```sh
    helm delete sysdig-agent -n ibm-observe
    ```
    {: pre}

    In Helm, `sysdig-agent` is the name of the release.
    {: tip}
