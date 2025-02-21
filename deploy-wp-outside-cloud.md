---

copyright:
  years:  2023
lastupdated: "2023-08-14"

keywords: IBM Cloud, deploy, Kubernetes, OpenShift

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Deploying the agent in an outside Kubernetes or OpenShift cluster
{: deploy-wp-outside-cloud}

In addition to its ability to run in {{site.data.keyword.cloud_notm}}, the centralized security and compliance framework that {{site.data.keyword.sysdigsecure_full}} provides can also be run in other clouds and on premises by using Helm charts to install the Workload Protect agent onto Kubernetes or OpenShift clusters.
{: shortdesc}

## Before you begin
{: deploy-wp-outside-cloud-before-begin}

* Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

   Helm 3.6 or later is required.
   {: note}

   [Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

* Check that you have access and permissions to deploy the {{site.data.keyword.sysdigsecure_short}} agent on the cluster. On a Kubernetes cluster, this means having the permission to run `kubectl` commands on the cluster. On an OpenShift cluster, this means have the permission to run `oc` commands. Check with the documentation of your cluster to learn more about getting the appropriate level of permissions and setting up your local machine to be able to properly issue commands to the cluster.

* Verify the `ibm-observe` namespace is available in your cluster. The agent is deployed in this namespace.

    You can run the following command to create the namespace: `kubectl create namespace ibm-observe`
    {: tip}

## Deploy an agent
{: deploy-wp-outside-cloud-deploy-agent}

Once you have a sufficient version of Helm and the permission to run commands on the cluster, you can use Helm to install, upgrade and delete the {{site.data.keyword.sysdigsecure_short}} on Kubernetes or OpenShift.

1. Add Sysdig as a repository for Helm charts on your local machine:

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

2. Update the repositories references by issuing `helm repo update`.

3. List the Helm charts that are currently available for the Sysdig repo.

    ```sh
    helm search repo sysdig
    ```
    {: pre}

4. Verify the Helm chart `sysdig/sysdig-deploy` is listed.

5. Install the {{site.data.keyword.sysdigsecure_short}}. This can be done by creating a yaml Helm values file where the values are listed and then issuing a command that references that file. 

    To install using a Helm values file, first create a file named `agent-values-monitor-secure.yaml` (or something similar). The following yaml is a template that you can use to configure the {{site.data.keyword.sysdigsecure_short}} agent. You can customize the file by removing or commenting with `#` the sections that are not required for your agent deployment.

```yaml
agent:
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
    log_level: info
    features:
      admission_control:
        enabled: true
      container_vulnerability_management:
        enabled: true
      audit:
        enabled: true
      posture:
        enabled: true
```
{: codeblock}

Where:

* `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
* `SERVICE_ACCESS_KEY` is the Workload Protection instance access key.
* `INGESTION_ENDPOINT` is the instance's ingestion endpoint. For example, `ingest.us-east.security-compliance-secure.cloud.ibm.com`
* `API_ENDPOINT` is the intance's API endpoint. For example, `us-east.security-compliance-secure.cloud.ibm.com`

Then, run the install command referencing the created Helm values file:

```sh
helm install -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
```
{: pre}

## Update an agent
{: deploy-wp-outside-cloud-update-agent}

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

With these steps, you'll upgrade your agents to the latest available version.

## Remove an agent
{: deploy-wp-outside-cloud-remove-agent}

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
