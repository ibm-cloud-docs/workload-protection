---

copyright:
  years:  2023, 2026
lastupdated: "2026-06-16"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent in a Kubernetes cluster by using a Helm chart
{: #agent-deploy-kube-helm}

You can use a Helm chart to install, upgrade, and delete a {{site.data.keyword.sysdigsecure_short}} agent on a Kubernetes cluster.
{: shortdesc}

You can also use the console to connect an existing {{site.data.keyword.redhat_openshift_notm}} or Kubernetes cluster to your instance of {{site.data.keyword.sysdigsecure_short}}. In the {{site.data.keyword.cloud_notm}} console, go to **Containers > Clusters** to access the existing cluster. Then, click **Connect** in the {{site.data.keyword.sysdigsecure_short}} widget to connect your cluster to {{site.data.keyword.sysdigsecure_short}}.
{: fast-path}

## Before you begin
{: #agent-deploy-kube-helm-prereqs}

- Install the {{site.data.keyword.cloud_notm}} CLI, the {{site.data.keyword.containershort_notm}} plug-in, and the {{site.data.keyword.registrylong_notm}} plug-in. For more information, go to [Installing the CLI](/docs/openshift?topic=openshift-cli-install).
- Install the latest release of the [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine. Helm version 3.6 or later is required. 


   [Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned to a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

- Verify that you have the required access and permissions to deploy the {{site.data.keyword.sysdigsecure_short}} agent on the cluster.
- Verify that the `ibm-observe` namespace is available in your cluster. The agent is deployed in this namespace.

    To create the namespace, run `kubectl create namespace ibm-observe`.
    {: tip}

- Verify that outbound traffic from your cluster to {{site.data.keyword.sysdigsecure_short}} endpoints is allowed on ports `443` and `6443`. If you connect the agents through a Virtual Private Endpoint (VPE), both ports must be allowed for outbound traffic from the cluster.

## Deploying an agent
{: #agent-deploy-kube-helm-deploy}

Complete the following steps to deploy an agent by using Helm.

### Set up the Sysdig Helm repository
{: #agent-deploy-kube-helm-install-step1}

Add the {{site.data.keyword.sysdigsecure_short}} Helm repository to your Helm instance.

1. Set the cluster context.

    ```sh
    ibmcloud ks cluster config --cluster <CLUSTER_NAME>
    ```
    {: pre}

2. Add the Helm repository.

    ```sh
    helm repo add sysdig https://charts.sysdig.com
    ```
    {: pre}

3. Update the repository to retrieve the latest versions of all Helm charts.

    ```sh
    helm repo update
    ```
    {: pre}

4. List the Helm charts that are currently available for the Sysdig repository.

    ```sh
    helm search repo sysdig
    ```
    {: pre}

5. Verify that the `sysdig/sysdig-deploy` Helm chart is listed.

### Create the values `YAML` file
{: #agent-deploy-kube-helm-install-step2}

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
{: #agent-deploy-kube-helm-install-step3}

To deploy the agent, the Secure components, or both, install the `sysdig/sysdig-deploy` chart. You can install the chart by using a variables `YAML` file like the one that you configured in the previous step, or you can configure the variables directly.

Run the following command to install the agent by using the Helm chart and the variables `YAML` file:

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
      api_url: https://private.us-east.security-compliance-secure.cloud.ibm.com
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
{: #agent-deploy-kube-helm-update}

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
{: #agent-deploy-kube-helm-delete}

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
