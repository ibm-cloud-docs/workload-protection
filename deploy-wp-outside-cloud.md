---

copyright:
  years:  2023, 2026
lastupdated: "2026-06-16"

keywords: IBM Cloud, deploy, Kubernetes, OpenShift

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Deploying the agent in an outside Kubernetes or {{site.data.keyword.redhat_openshift_notm}} cluster
{: #deploy-wp-outside-cloud}

In addition to its ability to run in {{site.data.keyword.cloud_notm}}, the centralized security and compliance framework that {{site.data.keyword.sysdigsecure_full}} provides can also be run in other clouds and on premises by using Helm charts to install the {{site.data.keyword.sysdigsecure_short}} agent onto Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters.
{: shortdesc}

## Before you begin
{: #deploy-wp-outside-cloud-before-begin}

- Install the latest release of the [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine. Helm version 3.6 or later is required. 

   [Helm](https://helm.sh){: external} is a Kubernetes package manager that uses Helm charts to define, install, and upgrade complex Kubernetes apps in your cluster. Helm charts package the specifications to generate YAML files for Kubernetes resources that build your app. These Kubernetes resources are automatically applied in your cluster and assigned to a version by Helm. You can also use Helm to specify and package your own app and let Helm generate the YAML files for your Kubernetes resources.

- Verify that you have the required access and permissions to deploy the {{site.data.keyword.sysdigsecure_short}} agent on the cluster. On a Kubernetes cluster, you must have permission to run `kubectl` commands on the cluster. On an {{site.data.keyword.redhat_openshift_notm}} cluster, you must have permission to run `oc` commands. Check with the documentation of your cluster to learn more about getting the appropriate level of permissions and setting up your local machine to issue commands to the cluster.

- Verify that the `ibm-observe` namespace is available in your cluster. The agent is deployed in this namespace.

    To create the namespace, run `kubectl create namespace ibm-observe`.
    {: tip}

- Verify that outbound traffic from your cluster to {{site.data.keyword.sysdigsecure_short}} endpoints is allowed on ports `443` and `6443`.

## Deploying an agent
{: #deploy-wp-outside-cloud-deploy-agent}

After you have a sufficient version of Helm and the permission to run commands on the cluster, you can use Helm to install, upgrade, and delete the {{site.data.keyword.sysdigsecure_short}} agent on Kubernetes or {{site.data.keyword.redhat_openshift_notm}}.

1. Add Sysdig as a repository for Helm charts on your local machine.

    ```sh
    helm repo add sysdig https://charts.sysdig.com
    ```
    {: pre}

    If you get the following error:

2. Update the repository references.

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

5. Install the {{site.data.keyword.sysdigsecure_short}} agent. You can install by creating a `YAML` Helm values file where the values are listed and then issuing a command that references that file.

    To install by using a Helm values file, first create a file named `agent-values-monitor-secure.yaml`. The following `YAML` is a template that you can use to configure the {{site.data.keyword.sysdigsecure_short}} agent. You can customize the file by removing or commenting with `#` the sections that are not required for your agent.

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

6. Then, run the install command that references the created Helm values file:

    ```sh
    helm install -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
    ```
    {: pre}

## Updating an agent
{: #deploy-wp-outside-cloud-update-agent}

To update the agent to the latest available version, complete the following steps:

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

## Removing an agent
{: #deploy-wp-outside-cloud-remove-agent}

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
