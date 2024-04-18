---

copyright:
  years:  2024
lastupdated: "2024-04-18"

keywords: workload protection, satellite, sysdig secure, manage

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent in a Satellite cluster by using a HELM chart
{: #agent-deploy-satellite}

You can use a Helm chart to install, upgrade, and delete a {{site.data.keyword.sysdigsecure_short}} components on your Satellite clusters.
{: shortdesc}

## Before you begin
{: #agent-deploy-satellite-prereqs}

- [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc`), and {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)](/docs/openshift?topic=openshift-cli-install).

- Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

   Helm 3.6 or later is required.
   {: note}

   [Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned to a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

- [Install the Red Hat OpenShift (oc) and Kubernetes (kubectl) CLIs](/docs/openshift?topic=openshift-cli-install#install-kubectl-cli).

- Check that you have access and permissions to deploy the {{site.data.keyword.sysdigsecure_short}} agent on the cluster.

- Verify the `ibm-observe` namespace is available in your cluster. The agent is deployed in this namespace. A project is a namespace in a cluster.

    You can run the following command to create the namespace: `oc adm new-project --node-selector='' ibm-observe`
    {: tip}

- Get your {{site.data.keyword.sysdigsecure_short}} `ingest` endpoint. This endpoint is different than the one being created in the next step. Access your Satellite location, then select **Link endpoints** and **System endpoints**. Copy the `system` endpoint starting with **satellite-sysdig-** that is pointing to `ingest.private.<region>.monitoring.cloud.ibm.com`. You can use this endpoint later as `INGESTION_SATELLITE_ENDPOINT`.

Before deploying the {{site.data.keyword.sysdigsecure_short}} components, create a [Satellite link endpoint](#agent-deploy-satellite-link-create) for the {{site.data.keyword.sysdigsecure_short}} private API endpoint. 

## Create {{site.data.keyword.sysdigsecure_short}} Satellite link endpoint
{: #agent-deploy-satellite-link-create}

Create an HTTPS [Satellite Link by using the console or CLI](/docs/satellite?topic=satellite-link-cloud-create) in order to connect securely to {{site.data.keyword.sysdigsecure_short}} private endpoints.

1. Get your {{site.data.keyword.sysdigsecure_short}} [private endpoint](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_monitoring). For example, if your {{site.data.keyword.sysdigsecure_short}} instance is in `us-east` your endpoint would be `private.us-east.security-compliance-secure.cloud.ibm.com`.

2. Access [**Satellite Locations** dashboard](https://cloud.ibm.com/satellite/locations). Link endpoints and click **Create an endpoint**.

3. Select **Cloud** to create an endpoint for a service, server, or app that runs outside of the location.

4. Enter an endpoint name, the destination domain name (FQDN) that should be the {{site.data.keyword.sysdigsecure_short}} private endpoint that is defined in step 1 and destination port 443.

5. Select the HTTPS protocol.

6. Click Create. Wait a few minutes for the **Satellite Link** connector component to assign a port to your endpoint.

7. In the table row for your endpoint, copy the hostname for your **Satellite Link** connector and the port for your endpoint in the **Address** field. You need to use it in the following steps.

You use this endpoint in the following steps as `API_ENDPOINT`.

## Deploy an agent
{: #agent-deploy-satellite-helm-deploy}

Complete the following steps to deploy an agent by using Helm:

### Step 1. Set up the cluster context
{: #agent-deploy-satellite-helm-install-step1}

1. Log in to the account. If you have a federated account, include the `--sso` option.

    ```sh
    ibmcloud login [-g <resource_group>] [--sso]
    ```
    {: pre}

2. Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable.

    ```sh
    ibmcloud oc cluster config --cluster <cluster_name_or_ID>
    ```
    {: pre}

3. In your browser, navigate to the address of your **Master URL** and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.

4. From the Red Hat OpenShift web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate via the CLI.

5. Verify that the `oc` commands run properly with your cluster by checking the version.

    ```sh
    oc version
    ```
    {: pre}

    Your output should look similar to this example:

    ```text
    Client Version: v4.11.0
    Kubernetes Version: v1.25.8.2
    ```
    {: screen}

### Step 2. Set up the Sysdig Helm repository
{: #agent-deploy-satellite-helm-install-step2}

Add the {{site.data.keyword.sysdigsecure_short}} Helm repository to your Helm instance.

Complete the following steps:

1. Set the cluster context.

    ```sh
    ibmcloud ks cluster config --cluster <CLUSTER_NAME>
    ```
    {: pre}

2.  Add the Helm repository.

    ```sh
    helm repo add sysdig https://charts.sysdig.com
    ```
    {: pre}

    If you get the following error:

    ```text
    helm repo add sysdig https://charts.sysdig.com    --debug
    Error: context deadline exceeded
    helm.go:84: [debug] context deadline exceeded
    ```
    {: screen}

    Run the following command and retry adding the Helm repository.

    ```sh
    rm $HOME/Library/Preferences/helm/repositories.lock
    ```
    {: pre}

3. Update the repos to retrieve the latest versions of all Helm charts.

    ```sh
    helm repo update
    ```
    {: pre}

4. List the Helm charts that are currently available for the Sysdig repo.

    ```sh
    helm search repo sysdig
    ```
    {: pre}

5. Verify that the Helm chart `sysdig/sysdig-deploy` is listed.

### Step 3. Create the Helm values file
{: #agent-deploy-satellite-helm-install-step3}

Define a yaml file and include the values to deploy the {{site.data.keyword.sysdigsecure_short}} components that you plan to deploy. For example, name the file `agent-values-monitor-secure.yaml`.

The following yaml is a template that you can use to configure the {{site.data.keyword.sysdigsecure_short}} components. You can customize the file by removing or commenting with `#` the sections that are not required for your agent deployment.

```yaml
agent:
  collectorSettings:
    collectorHost: INGESTION_SATELLITE_ENDPOINT
    collectorPort: INGESTION_SATELLITE_ENDPOINT_PORT
  slim:
    enabled: true
global:
  clusterConfig:
    name: CLUSTER_NAME
  kspm:
    deploy: true
  sysdig:
    accessKey: SERVICE_ACCESS_KEY
    apiHost: API_ENDPOINT
nodeAnalyzer:
  secure: 
    vulnerabilityManagement:
      newEngineOnly: true
  nodeAnalyzer:
    runtimeScanner: 
      deploy: false
    benchmarkRunner:
      deploy: false
    hostScanner:
      deploy: false
    deploy: true
  natsUrl: wss://API_ENDPOINT
  sslVerifyCertificate: false
kspmCollector:
  natsUrl: wss://API_ENDPOINT
  sslVerifyCertificate: false
clusterScanner:
  enabled: true
  eveEnabled: true
  sslVerifyCertificate: false
```
{: codeblock}

Where:

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `SERVICE_ACCESS_KEY` is the {{site.data.keyword.sysdigsecure_short}} instance access key.
- `INGESTION_SATELLITE_ENDPOINT` is the [Satellite endpoint extracted previously](#agent-deploy-satellite-link-create) that points to Ingest endpoint. For example, `c1bcda0323e0ef4b83aba-6b64a6ccc9c596bf59a86625d8fa2202-c111.us-east.satellite.appdomain.cloud`.
- `INGESTION_SATELLITE_ENDPOINT_PORT` is the port from the [Satellite endpoint extracted previously](#agent-deploy-satellite-link-create) that points to `ingest` endpoint. For example, `30771`.
- `API_ENDPOINT` is the [Satellite endpoint extracted previously](#agent-deploy-satellite-link-create) that points to {{site.data.keyword.sysdigsecure_short}} private API endpoint. For example, `c1bcda0323e0ef4b83aba-6b64a6ccc9c596bf59a86625d8fa2202-c111.us-east.satellite.appdomain.cloud:31924`. In this case, both hostname and port are defined together.


### Step 4. Install the Helm chart
{: #agent-deploy-satellite-helm-install-step4}

To deploy the agent, the {{site.data.keyword.sysdigsecure_short}} components, or both, you must install the `sysdig/sysdig-deploy` chart and use the variables yaml file that you configured in the previous step.

Run the following command to install the agent by using the Helm chart:

```sh
helm install -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
```
{: pre}

If you want to directly install the {{site.data.keyword.sysdigsecure_short}} components **without a Helm values file**, you can run the following command setting all variables with `--set`.

```sh
helm install sysdig-agent sysdig/sysdig-deploy --namespace ibm-observe --create-namespace\
    --set global.sysdig.accessKey=<SERVICE_ACCESS_KEY> \
    --set global.sysdig.apiHost=<API_ENDPOINT> \
    --set agent.collectorSettings.collectorHost=<INGESTION_SATELLITE_ENDPOINT> \
    --set agent.collectorSettings.collectorPort=<INGESTION_SATELLITE_ENDPOINT_PORT> \
    --set nodeAnalyzer.natsUrl=wss://<API_ENDPOINT> \
    --set nodeAnalyzer.nodeAnalyzer.runtimeScanner.deploy=false \
    --set nodeAnalyzer.nodeAnalyzer.hostScanner.deploy=false \
    --set nodeAnalyzer.nodeAnalyzer.benchmarkRunner.deploy=false \
    --set nodeAnalyzer.nodeAnalyzer.sslVerifyCertificate=false \
    --set nodeAnalyzer.secure.vulnerabilityManagement.newEngineOnly=true \
    --set global.kspm.deploy=true \
    --set global.clusterConfig.name=<CLUSTER_NAME> \
    --set kspmCollector.natsUrl=wss://<API_ENDPOINT> \
    --set kspmCollector.sslVerifyCertificate=false \
    --set clusterScanner.enabled=true \
    --set clusterScanner.eveEnabled=true \
    --set clusterScanner.sslVerifyCertificate=true 
```
{: pre}

Where:

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `SERVICE_ACCESS_KEY` is the {{site.data.keyword.sysdigsecure_short}} instance access key.
- `INGESTION_SATELLITE_ENDPOINT` is the [Satellite endpoint extracted previously](#agent-deploy-satellite-link-create) that points to `ingest` endpoint. For example, `c1bcda0323e0ef4b83aba-6b64a6ccc9c596bf59a86625d8fa2202-c111.us-east.satellite.appdomain.cloud`.
- `INGESTION_SATELLITE_ENDPOINT_PORT` is the port from the [Satellite endpoint extracted previously](#agent-deploy-satellite-link-create) that points to the `ingest` endpoint. For example, `30771`.
- `API_ENDPOINT` is the [Satellite endpoint extracted previously](#agent-deploy-satellite-link-create) that points to {{site.data.keyword.sysdigsecure_short}} private API endpoint. For example, `c1bcda0323e0ef4b83aba-6b64a6ccc9c596bf59a86625d8fa2202-c111.us-east.satellite.appdomain.cloud:31924`. In this case, both hostname and port are defined together.

## Update an agent
{: #agent-deploy-satellite-kube-helm-update}

We recommend updating the {{site.data.keyword.sysdigsecure_short}} at least once every 2 months.

To update the agent version by using Helm, complete the following steps:

1. Update the chart.

    ```sh
    helm repo update
    ```
    {: pre}

2. Upgrade the agent.

    ```sh
    helm upgrade -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
    ```
    {: pre}

## Remove an agent
{: #agent-deploy-satellite-kube-helm-delete}

To delete the agent by using Helm, you must uninstall the chart.

Complete the following steps:

1. List the charts that are installed.

    ```sh
    helm list -n ibm-observe
    ```
    {: pre}

    The output of the command lists charts as follows:

    ```text
    NAME        	NAMESPACE  	REVISION	UPDATED                             	STATUS  	CHART              	  APP VERSION
    sysdig-agent	ibm-observe	1       	2023-03-24 15:02:58.408108 +0100 CET	deployed	sysdig-deploy-1.37.10
    ```
    {: screen}

2. Uninstall the chart.

    ```sh
    helm delete sysdig-agent  -n ibm-observe
    ```
    {: pre}

    In terms of Helm, `sysdig-agent` is the name of the release.
    {: tip}


    If you forget to include the namespace in the command, you get the following error: `Error: uninstall: Release not loaded: sysdig-agent: release: not found`.
