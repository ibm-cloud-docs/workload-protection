---

copyright:
  years:  2023
lastupdated: "2023-09-27"


keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Managing the {{site.data.keyword.sysdigsecure_short}} agent in a Kubernetes cluster by using a HELM chart
{: #agent-deploy-kube-helm}


You can use a Helm chart to install, upgrade, and delete a {{site.data.keyword.sysdigsecure_short}} agent on a Kubernetes cluster.
{: shortdesc}



## Before you begin
{: #agent-deploy-kube-helm-prereqs}

- [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc`), and {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)](/docs/openshift?topic=openshift-openshift-cli#cs_cli_install_steps)

- Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

   Helm 3.6 or later is required.
   {: note}

   [Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

- Check that you have access and permissions to deploy the {{site.data.keyword.sysdigsecure_short}} agent on the cluster.

- Verify the `ibm-observe` namespace is available in your cluster. The agent is deployed in this namespace.

    You can run the following command to create the namespace: `kubectl create namespace ibm-observe`
    {: tip}

## Deploy an agent
{: #agent-deploy-kube-helm-deploy}

Complete the following steps to deploy an agent by using Helm:

### Step 1. Setup the Sysdig Helm repository
{: #agent-deploy-kube-helm-install-step1}

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

5. Verify the Helm chart `sysdig/sysdig-deploy` is listed.






### Step 2. Create the values yaml file
{: #agent-deploy-kube-helm-install-step2}

Define a yaml file and include the values to deploy the {{site.data.keyword.sysdigsecure_short}} agent and the Secure components that you plan to deploy. For example, name the file `agent-values-monitor-secure.yaml`.

The following yaml is a template that you can use to configure the {{site.data.keyword.sysdigsecure_short}} agent and the Secure components. You can customize the file by removing or commenting with `#` the sections that are not required for your agent deployment.

```yaml
global:
  clusterConfig:
    name: CLUSTER_NAME
  sysdig:
    accessKey: SERVICE_ACCESS_KEY
  kspm:
    deploy: true
agent:
  image:
    registry: icr.io
  slim:
    enabled: true
    image:
      repository: ext/sysdig/agent-slim
    kmoduleImage:
      repository: ext/sysdig/agent-kmodule
  collectorSettings:
    collectorHost: INGESTION_ENDPOINT
nodeAnalyzer:
  secure: vulnerabilityManagement:
    newEngineOnly: true
  nodeAnalyzer:
    runtimeScanner: settings:
      eveEnabled: true
    deploy: true
    apiEndpoint: API_ENDPOINT
    benchmarkRunner:
      deploy: false
kspmCollector:
  apiEndpoint: API_ENDPOINT
```
{: codeblock}

Where

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `SERVICE_ACCESS_KEY` is the {{site.data.keyword.sysdigsecure_short}} instance access key.
- `INGESTION_ENDPOINT` is the instance's ingestion endpoint. For example, `ingest.us-east.security-compliance-secure.cloud.ibm.com`
- `API_ENDPOINT` is the intance's API endpoint. For example, `us-east.security-compliance-secure.cloud.ibm.com`



### Step 3. Install the Helm chart
{: #agent-deploy-kube-helm-install-step3}

To deploy the agent, the Secure components, or both, you must install the `sysdig/sysdig-deploy` chart. You can install the chart by using a variables yaml file like the one that you configured in the previous step, or you can configure the variables directly.

Run the following command to install the agent by using the helm chart and the variables yaml file:

```sh
helm install -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
```
{: pre}


Run the following command to install the agent by using the helm chart and setting the variables:

```sh
helm install sysdig-agent sysdig/sysdig-deploy --namespace ibm-observe --create-namespace\
    --set global.sysdig.accessKey=<SERVICE_ACCESS_KEY> \
    --set agent.collectorSettings.collectorHost=<INGESTION_ENDPOINT> \
    --set nodeAnalyzer.nodeAnalyzer.apiEndpoint=<API_ENDPOINT> \
    --set nodeAnalyzer.nodeAnalyzer.runtimeScanner.settings.eveEnabled=true \
    --set nodeAnalyzer.secure.vulnerabilityManagement.newEngineOnly=true \
    --set global.kspm.deploy=true \
    --set nodeAnalyzer.nodeAnalyzer.benchmarkRunner.deploy=false \
    --set global.clusterConfig.name=<CLUSTER_NAME> \
    --set kspmCollector.apiEndpoint=<API_ENDPOINT> \
    --set agent.image.registry=icr.io \
    --set agent.slim.image.repository=ext/sysdig/agent-slim \
    --set agent.slim.kmoduleImage.repository=ext/sysdig/agent-kmodule
```
{: pre}

Where

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `SERVICE_ACCESS_KEY` is the {{site.data.keyword.sysdigsecure_short}} instance access key.
- `INGESTION_ENDPOINT` is the instance's ingestion endpoint.
- `API_ENDPOINT` is the intance's API endpoint.


For example, for the US-East region, a sample Helm install looks as follows:

```sh
helm install sysdig-agent sysdig/sysdig-deploy --namespace ibm-observe \
    --set global.sysdig.accessKey=<ENTER_YOUR_ACCESS_KEY> \
    --set agent.collectorSettings.collectorHost=ingest.us-east.security-compliance-secure.cloud.ibm.com \
    --set nodeAnalyzer.nodeAnalyzer.apiEndpoint=us-east.security-compliance-secure.cloud.ibm.com  \
    --set global.kspm.deploy=true \
    --set nodeAnalyzer.nodeAnalyzer.benchmarkRunner.deploy=false \
    --set global.clusterConfig.name=mycluster-au-syd \
    --set kspmCollector.apiEndpoint=us-east.security-compliance-secure.cloud.ibm.com \
    --set agent.image.registry=icr.io \
    --set agent.slim.image.repository=ext/sysdig/agent-slim \
    --set agent.slim.kmoduleImage.repository=ext/sysdig/agent-kmodule
```
{: pre}


If you encounter the following error: `Error: INSTALLATION FAILED: Kubernetes cluster unreachable: xxxxxx failed to refresh token: oauth2: cannot fetch token: 400 Bad Request`, set your cluster context and try again.



## Update an agent
{: #agent-deploy-kube-helm-update}

To update the agent version by using Helm, complete the following steps:

1. Update the chart.

    ```sh
    helm repo update
    ```
    {: pre}

2. Find the values yaml file that you used to deploy the agent and modify the `agent.image.tag` with the version of the agent that you want to deploy.

3. Upgrade the agent.

    ```sh
    helm upgrade -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
    ```
    {: pre}



## Remove an agent
{: #agent-deploy-kube-helm-delete}

To delete the agent by using Helm, you must uninstall the chart.

Complete the following steps:

1. List the charts that are installed.

    ```sh
    helm list -n ibm-observe
    ```
    {: pre}

    The output of the command lists charts as follows:

    ```text
    NAME        	NAMESPACE  	REVISION	UPDATED                             	STATUS  	CHART              	APP VERSION
    sysdig-agent	ibm-observe	1       	2023-03-24 15:02:58.408108 +0100 CET	deployed	sysdig-deploy-1.6.3
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
