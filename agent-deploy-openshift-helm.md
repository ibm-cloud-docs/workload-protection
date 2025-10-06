---

copyright:
  years:  2023, 2024
lastupdated: "2024-04-18"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing the {{site.data.keyword.sysdigsecure_short}} agent in {{site.data.keyword.redhat_openshift_notm}} by using a HELM chart
{: #agent-deploy-openshift-helm}

You can use a Helm chart to install, upgrade, and delete a {{site.data.keyword.sysdigsecure_short}} agent on a {{site.data.keyword.redhat_openshift_notm}} cluster.
{: shortdesc}

## Before you begin
{: #agent-deploy-openshift-helm-prereqs}

- Install the latest release of the version 3 [Helm CLI](https://github.com/helm/helm/releases){: external} on your local machine.

   Helm 3.6 or later is required.
   {: note}

- [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc`), and {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)](/docs/openshift?topic=openshift-cli-install).

- [Install the {{site.data.keyword.redhat_openshift_notm}} (`oc`) and Kubernetes (`kubectl`) CLIs](/docs/openshift?topic=openshift-cli-install#install-kubectl-cli).

- Check that you have access and permissions to deploy the {{site.data.keyword.sysdigsecure_short}} agent on the cluster.

- Verify the `ibm-observe` project is available in your cluster. The agent is deployed in this project.

    A project is a namespace in a cluster.

    You can run `oc adm new-project --node-selector='' ibm-observe` to create the project.
    {: tip}

- Outbound traffic from your cluster to {{site.data.keyword.sysdigsecure_short}} endpoints is required to port `443` and `6443`. Similarly, if you connect the agents via VPE, both ports need to be allowed for outbound traffic from the cluster.

## Deploy an agent
{: #agent-deploy-openshift-helm-deploy}

Complete the following steps to deploy an agent by using Helm:

### Step 1. Set up the cluster context
{: #agent-deploy-openshift-helm-install-step1}

Complete the following steps:

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

4. From the {{site.data.keyword.redhat_openshift_notm}} web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate from the CLI.

5. Verify that the `oc` commands run properly with your cluster by checking the version.

    ```sh
    oc version
    ```
    {: pre}

    Example output

    ```sh
    Client Version: v4.11.0
    Kubernetes Version: v1.25.8.2
    ```
    {: screen}

    If you can't perform operations that require Administrator permissions, such as listing all the worker nodes or pods in a cluster, download the TLS certificates and permission files for the cluster administrator by running the `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` command.
    {: tip}

### Step 2. Setup the Sysdig Helm repository
{: #agent-deploy-openshift-helm-install-step2}

Add the {{site.data.keyword.sysdigsecure_short}} Helm repository to your Helm instance.

1.  Add the Helm repository.

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


2. Update the repos to retrieve the latest versions of all Helm charts.

    ```sh
    helm repo update
    ```
    {: pre}

3. List the Helm charts that are currently available for the Sysdig repo.

    ```sh
    helm search repo sysdig
    ```
    {: pre}

4. Verify the Helm chart `sysdig/sysdig-deploy` is listed.






### Step 3. Create the values yaml file
{: #agent-deploy-openshift-helm-install-step3}

Define a yaml file and include the values to deploy the {{site.data.keyword.sysdigsecure_short}} agent and the Secure components that you plan to deploy. For example, name the file `agent-values-monitor-secure.yaml`.

The following yaml is a template that you can use to configure the {{site.data.keyword.sysdigsecure_short}} agent and the Secure components. You can customize the file by removing or commenting with `#` the sections that are not required for your agent deployment.

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

Where

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `SERVICE_ACCESS_KEY` is the {{site.data.keyword.sysdigsecure_short}} instance access key.
- `INGESTION_ENDPOINT` is the instance's ingestion endpoint. For example, `ingest.us-east.security-compliance-secure.cloud.ibm.com`
- `API_ENDPOINT` is the intance's API endpoint. For example, `us-east.security-compliance-secure.cloud.ibm.com`

   The `universal_ebpf` driver requires kernel version 5.8 or newer. If you have a lower version you need BPF ring buffer support and a kernel that exposes BTF (BPF Type Format). If you have any problem during the agent installation, try removing the lines `agent.ebpf.enabled: true` and `agent.ebpf.kind: universal_ebpf` or [contact support](/docs/workload-protection?topic=workload-protection-gettinghelp).
   {: note}

### Step 4. Install the helm chart
{: #agent-deploy-openshift-helm-install-step4}

To deploy the agent, the Secure components, or both, you must install the `sysdig/sysdig-deploy` chart and use the variables yaml file that you configured in the previous step.

Run the following command to install the agent by using the helm chart:

```sh
helm install -n ibm-observe sysdig-agent sysdig/sysdig-deploy -f agent-values-monitor-secure.yaml
```
{: pre}

For example, for the us-east region, a sample Helm values file looks as follows:

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
{: pre}

Where

- `CLUSTER_NAME` is the name of the cluster where you are deploying the agent.
- `SERVICE_ACCESS_KEY` is the {{site.data.keyword.sysdigsecure_short}} instance access key.
- `INGESTION_ENDPOINT` is the instance's ingestion endpoint.
- `API_ENDPOINT` is the intance's API endpoint.



If you encounter the following error: `Error: INSTALLATION FAILED: OpenShift cluster unreachable: xxxxxx failed to refresh token: oauth2: cannot fetch token: 400 Bad Request`, set your cluster context and try again.



## Update an agent
{: #agent-deploy-openshift-helm-update}

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
{: #agent-deploy-openshift-helm-delete}

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
