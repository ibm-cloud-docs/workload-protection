---

copyright:
  years:  2023
lastupdated: "2023-05-08"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Helm charts configurable parameters (WIP)
{: #agent-helm-parameters}

You can use {{site.data.keyword.sysdigsecure_short}} API tokens to authenticate with the {{site.data.keyword.sysdigsecure_full_notm}} service when you use Python scripts or the {{site.data.keyword.sysdigsecure_full_notm}} REST API to automate routine tasks and monitor notifications.
{: shortdesc}

Consider the following information for each instance of the {{site.data.keyword.sysdigsecure_full_notm}} service:



The following table lists the configurable parameters of the sysdig-deploy chart and their default values.

The sysdig-deploy chart itself only has select parameters that are used by multiple subcharts, and those are used to enable/disable selected subcharts.

If you need additional configuration values, those are available in the various READMEs of the individual subcharts (admission-controller, agent, node-analyzer, kspm-collector and rapid-response).




## Parameters of the sysdig-deploy chart



| Parameter                                                   | Description        | Default |
|-------------------------------------------------------------|--------------------|----------------|
| `namespace`                                                 | The namespace or project where the agent is deployed in the cluster. | `ibm-observe` |
| `global.clusterConfig.name`                                 | Name of the cluster where you are deploying the agent.  |	|
| `global.sysdig.accessKey`                                   | {{site.data.keyword.sysdigsecure_short}} instance access key. |	 |
| `global.sysdig.accessKeySecret`                             | 	The name of a Kubernetes secret containing an ‘access-key’ entry 	""
| `global.sysdig.secureAPIToken`                              | 	API Token to access Sysdig Secure 	""
| `global.sysdig.secureAPITokenSecret`                        | 	The name of a Kubernetes secret containing API Token to access Sysdig Secure 	""
| `global.sysdig.tags`                                        | 	Sets the global tags which can override agent tags 	{}
| `global.imageRegistry`                                      | 	Container image registry 	``
| `global.proxy.httpProxy`                                    | 	Sets http_proxy on the Agent container 	""
| `global.proxy.httpsProxy`                                   | 	Sets https_proxy on the Agent container 	""
| `global.proxy.noProxy`                                      | 	Sets no_proxy on the Agent container 	""
| `global.kspm.deploy`                                        | 	Enables Sysdig KSPM node analyzer & KSPM collector 	false
| `global.agentConfigmapName`                                 | 	Sets a configmap name that is used to mount the agent configmap to fetch the cluster name and agent tags 	"sysdig-agent"
| `admissionController`                                       | 	Config specific to the Sysdig AdmissionController 	{}
| `admissionController.enabled`                               | 	Enable the admission controller component in this chart 	false
| `agent`                                                     | 	Config specific to the Sysdig Agent 	{}
| `agent.enabled`                                             | 	Enable the agent component in this chart 	true
| `nodeAnalyzer`                                              | 	Config specific to the Sysdig nodeAnalyzer 	{}
| `nodeAnalyzer.enabled`                                      | 	Enable the nodeAnalyzer component in this chart 	true
| `nodeAnalyzer.secure.enabled`                               | 	Enable Sysdig Secure 	true
| `nodeAnalyzer.secure.vulnerabilityManagement.newEngineOnly` | 	Enable only the new vulnerability management engine 	false
| `nodeAnalyzer.nodeAnalyzer.apiEndpoint`                     | 	nodeAnalyzer apiEndpoint 	""
| `nodeAnalyzer.nodeAnalyzer.benchmarkRunner.deploy`          | 	Deploy the Benchmark Runner Scanner 	true
| `nodeAnalyzer.nodeAnalyzer.runtimeScanner.deploy`           | 	Deploy the Runtime Scanner 	false
| `kspmCollector`                                             | 	Config specific to the Sysdig KSPM Collector 	{}
| `kspmCollector.apiEndpoint`                                 | 	kspmCollector apiEndpoint 	""
| `rapidResponse`                                             | 	Config specific to Sysdig Rapid Response 	{}
| `rapidResponse.enabled`                                     | 	Enable Rapid Response component in this chart 	""



    --set agent.collectorSettings.collectorHost=ingest.us-east.monitoring.cloud.ibm.com \
    --set nodeAnalyzer.nodeAnalyzer.apiEndpoint=us-east.monitoring.cloud.ibm.com \
    --set nodeAnalyzer.secure.vulnerabilityManagement.newEngineOnly=true \
    --set global.kspm.deploy=true \
    --set nodeAnalyzer.nodeAnalyzer.benchmarkRunner.deploy=false \


## Agent deployment

For configuration values of the agent, see the Agent subchart README. Prefix all the specific configurations with agent. to apply them to the chart.

Example: override proxy variable for Agent chart

As a command line parameter:

helm install sysdig sysdig/sysdig-deploy \
    --namespace sysdig-agent \
    --set global.sysdig.accessKey=ACCESS_KEY \
    --set global.sysdig.region=SAAS_REGION \
    --set global.clusterConfig.name=CLUSTER_NAME \
    --set global.proxy.httpProxy=PROXY_URL \
    --set agent.proxy.httpProxy=OVERRIDE_PROXY_URL
