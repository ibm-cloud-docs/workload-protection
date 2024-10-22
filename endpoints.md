---

copyright:
  years:  2023
lastupdated: "2023-10-16"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Endpoints
{: #endpoints}

A list of supported public and private endpoints for the {{site.data.keyword.sysdigsecure_full_notm}} service.
{: shortdesc}



## Web UI endpoints
{: #endpoints_monitoring}

To access the {{site.data.keyword.sysdigsecure_full_notm}} web UI, you might need to define a firewall rule in your host.
{: note}


The following table lists the endpoints that are available for each region:

| Region      | Web UI endpoint                                  | Public IP addresses                                       |  Ports           |
|-------------|--------------------------------------------------|-----------------------------------------------------------|-----------------|
| `US-SOUTH`  | `https://us-south.security-compliance-secure.cloud.ibm.com`      | 169.60.151.174  \n 169.46.0.70  \n 169.48.214.70        | https (TLS) 443 |
| `EU-DE`     | `https://eu-de.security-compliance-secure.cloud.ibm.com`         | 149.81.77.78  \n 161.156.102.206  \n 159.122.102.38     | https (TLS) 443 |
| `EU-GB`     | `https://eu-gb.security-compliance-secure.cloud.ibm.com`         | 158.175.98.206  \n 141.125.73.118  \n 159.122.210.174   | https (TLS) 443 |
| `JP-OSA`    | `https://jp-osa.security-compliance-secure.cloud.ibm.com`        | 163.68.67.98  \n 163.69.66.170  \n 163.73.67.180 | https (TLS) 443 |
| `JP-TOK`    | `https://jp-tok.security-compliance-secure.cloud.ibm.com`        | 165.192.84.14  \n 128.168.75.14  \n 169.56.51.238       | https (TLS) 443 |
| `US-EAST`   | `https://us-east.security-compliance-secure.cloud.ibm.com`       | 169.60.112.74  \n 169.55.109.114  \n 169.62.3.82        | https (TLS) 443 |
| `AU-SYD`    | `https://au-syd.security-compliance-secure.cloud.ibm.com`        | 135.90.73.100  \n 130.198.80.155  \n 168.1.213.78       | https (TLS) 443 |
| `CA-TOR`    | `https://ca-tor.security-compliance-secure.cloud.ibm.com`        | 163.74.69.186  \n 158.85.94.130  \n 163.75.65.237       | https (TLS) 443 |
| `BR-SAO`    | `https://br-sao.security-compliance-secure.cloud.ibm.com`        | 163.107.66.98  \n 163.109.67.242  \n 169.57.141.43       | https (TLS) 443 |
{: caption="List of endpoints" caption-side="top"}




## REST API endpoints
{: #endpoints_rest_api}

To make API calls, you might need to define a firewall rule in your host.
{: note}

### Private REST API endpoints
{: #endpoints_rest_api_private}

| Region      | Private REST API endpoint                                     |
|-------------|---------------------------------------------------------------|
| `US-SOUTH`  | `https://private.us-south.security-compliance-secure.cloud.ibm.com/api`      |
| `EU-DE`     | `https://private.eu-de.security-compliance-secure.cloud.ibm.com/api`         |
| `EU-GB`     | `https://private.eu-gb.security-compliance-secure.cloud.ibm.com/api`         |
| `JP-OSA`    | `https://private.jp-osa.security-compliance-secure.cloud.ibm.com/api`         |
| `JP-TOK`    | `https://private.jp-tok.security-compliance-secure.cloud.ibm.com/api`        |
| `US-EAST`   | `https://private.us-east.security-compliance-secure.cloud.ibm.com/api`       |
| `AU-SYD`    | `https://private.au-syd.security-compliance-secure.cloud.ibm.com/api`        |
| `CA-TOR`    | `https://private.ca-tor.security-compliance-secure.cloud.ibm.com/api`        |
| `BR-SAO`    | `https://private.br-sao.security-compliance-secure.cloud.ibm.com/api`        |
{: caption="Private REST API endpoints for the {{site.data.keyword.sysdigsecure_full_notm}} service" caption-side="top"}


### Public REST API endpoints
{: #endpoints_rest_api_public}


| Region      | Public REST API endpoint                                      |
|-------------|---------------------------------------------------------------|
| `US-SOUTH`  | `https://us-south.security-compliance-secure.cloud.ibm.com/api`      |
| `EU-DE`     | `https://eu-de.security-compliance-secure.cloud.ibm.com/api`         |
| `EU-GB`     | `https://eu-gb.security-compliance-secure.cloud.ibm.com/api`         |
| `JP-OSA`    | `https://jp-osa.security-compliance-secure.cloud.ibm.com/api`        |
| `JP-TOK`    | `https://jp-tok.security-compliance-secure.cloud.ibm.com/api`        |
| `US-EAST`   | `https://us-east.security-compliance-secure.cloud.ibm.com/api`       |
| `AU-SYD`    | `https://au-syd.security-compliance-secure.cloud.ibm.com/api`        |
| `CA-TOR`    | `https://ca-tor.security-compliance-secure.cloud.ibm.com/api`        |
| `BR-SAO`    | `https://br-sao.security-compliance-secure.cloud.ibm.com/api`        |
{: caption="Public REST API endpoints for the {{site.data.keyword.sysdigsecure_full_notm}} service" caption-side="top"}




## Collector endpoints
{: #endpoints_ingestion}

Collector endpoints are ingestion endpoints that you can use to send data.


### Private Collector endpoints
{: #endpoints_ingestion_private}

To send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account.
{: note}

The following table lists the *Private Collector endpoints* that are available for each region:

| Region      | Private ingestion endpoint       | Private IP addresses       | Workload Protection  \n  agent ports   | Prometheus  \n  Remote Write  \n Ports|
|-------------|----------------------------------|----------------------------|-----------|---------|
| Dallas (`US-South`)  | `ingest.private.us-south.security-compliance-secure.cloud.ibm.com`   | 166.9.14.170  \n 166.9.48.41  \n 166.9.17.11   \n  \n 166.9.228.45 `(*)`  \n 166.9.229.45 `(*)`  \n 166.9.230.44 `(*)`   | TCP 6443  | TCP 443  |
| Frankfurt (`EU-DE`)     | `ingest.private.eu-de.security-compliance-secure.cloud.ibm.com`      | 166.9.32.51  \n 166.9.30.53  \n 166.9.28.71   \n  \n  166.9.248.88 `(*)`  \n 166.9.248.120 `(*)`  \n 166.9.248.152 `(*)`     | TCP 6443  | TCP 443  |
| London (`EU-GB`)     | `ingest.private.eu-gb.security-compliance-secure.cloud.ibm.com`      | 166.9.34.56  \n 166.9.36.71   \n  \n  166.9.244.29 `(*)`  \n 166.9.244.59 `(*)`                       |  TCP 6443 | TCP 443  |
| Madrid (`EU-ES`)     | `ingest.private.eu-es.security-compliance-secure.cloud.ibm.com`      | 166.9.96.31  \n 166.9.95.31  \n 166.9.94.31   \n  \n  166.9.226.17 `(*)`  \n 166.9.227.16 `(*)`   \n 166.9.225.16 `(*)`         |  TCP 6443 | TCP 443  |
| Osaka (`JP-OSA`)    | `ingest.private.jp-osa.security-compliance-secure.cloud.ibm.com`     | 166.9.72.14  \n 166.9.71.15  \n 166.9.70.14   \n  \n  166.9.247.44 `(*)`  \n 166.9.247.77 `(*)`  \n 166.9.247.109 `(*)`  | TCP 6443 |  TCP 443  |
| Sao Paulo (`BR-SAO`)  | `ingest.private.br-sao.security-compliance-secure.cloud.ibm.com`   | 166.9.84.19  \n 166.9.83.18  \n 166.9.82.19   \n  \n  166.9.246.77 `(*)`  \n 166.9.246.108 `(*)`  \n 166.9.246.133 `(*)`   | TCP 6443  |  TCP 443  |
| Sydney (`AU-SYD`)    | `ingest.private.au-syd.security-compliance-secure.cloud.ibm.com`     | 166.9.56.32  \n 166.9.52.27   \n 166.9.54.27  \n  \n  166.9.244.114 `(*)`  \n 166.9.244.144 `(*)`  \n 166.9.244.177 `(*)`      |  TCP 6443 |  TCP 443  |
| Tokyo (`JP-TOK`)    | `ingest.private.jp-tok.security-compliance-secure.cloud.ibm.com`     | 166.9.44.38  \n 166.9.40.35  \n 166.9.42.48  \n  \n  166.9.249.112 `(*)`  \n 166.9.249.141 `(*)`  \n 166.9.249.177 `(*)`         | TCP 6443  |  TCP 443  |
| Toronto (`CA-TOR`)  | `ingest.private.ca-tor.security-compliance-secure.cloud.ibm.com`   | 166.9.77.20  \n 166.9.76.23  \n 166.9.78.21  \n  \n  166.9.247.153 `(*)`  \n 166.9.247.185 `(*)`  \n 166.9.247.205 `(*)`    | TCP 6443  |  TCP 443  |
| Washington (`US-East`)   | `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`    | 166.9.22.50  \n 166.9.24.43  \n 166.9.20.53  \n  \n  166.9.231.240 `(*)`  \n 166.9.232.28 `(*)`  \n 166.9.233.17 `(*)`       | TCP 6443  |  TCP 443  |
{: caption="List of ingestion endpoints and private IP addresses to send data to the {{site.data.keyword.mon_full_notm}}" caption-side="top"}

`(*)` Indicates IP addresses that are in plan to be supported. These IP addresses should be added to an allowlist in advance to avoid service interruptions. Current IP addresses will be deprecated. A notification will be sent before the current IP addresses are deprecated.
{: note}


### Public Collector endpoints
{: #endpoints_ingestion_public}

The following table lists the *Public Collector endpoints* that are available for each region:

| Region      | Public ingestion endpoint      | Public IP addresses    | {{site.data.keyword.sysdigsecure_full_notm}} agent ports   |
|-------------|-------------------------------|-------------------------|---------|
| `US-SOUTH`  | `ingest.us-south.security-compliance-secure.cloud.ibm.com`          | 169.60.151.174  \n 169.46.0.70  \n 169.48.214.70      | TCP 6443 |
| `EU-DE`     | `ingest.eu-de.security-compliance-secure.cloud.ibm.com`             | 149.81.77.78  \n 161.156.102.206  \n 159.122.102.38   | TCP 6443 |
| `EU-GB`     | `ingest.eu-gb.security-compliance-secure.cloud.ibm.com`             | 158.175.98.206  \n 141.125.73.118  \n 159.122.210.174 | TCP 6443 |
| `JP-OSA`    | `ingest.jp-osa.security-compliance-secure.cloud.ibm.com`            | 163.68.67.98  \n 163.69.66.170  \n 163.73.67.180 | TCP 6443 |
| `JP-TOK`    | `ingest.jp-tok.security-compliance-secure.cloud.ibm.com`            | 165.192.84.14  \n 128.168.75.14  \n 169.56.51.238     | TCP 6443 |
| `US-EAST`   | `ingest.us-east.security-compliance-secure.cloud.ibm.com`           | 169.60.112.74  \n 169.55.109.114  \n 169.62.3.82      | TCP 6443 |
| `AU-SYD`    | `ingest.au-syd.security-compliance-secure.cloud.ibm.com`            | 135.90.73.100  \n 130.198.80.155  \n 168.1.213.78     | TCP 6443 |
| `CA-TOR`    | `ingest.ca-tor.security-compliance-secure.cloud.ibm.com`            | 163.74.69.186  \n 158.85.94.130  \n 163.75.65.237     | TCP 6443 |
| `BR-SAO`    | `ingest.br-sao.security-compliance-secure.cloud.ibm.com`            | 163.107.66.98  \n 163.109.67.242  \n 169.57.141.43     | TCP 6443 |
{: caption="List of ingestion endpoints and public IP addresses to send data to the {{site.data.keyword.sysdigsecure_full_notm}}" caption-side="top"}


## Subnets for webhook notifications from {{site.data.keyword.sysdigsecure_full_notm}}
{: #endpoints_network_alert_subnets}

To receive alert notifications by using webhooks from the {{site.data.keyword.sysdigsecure_full_notm}} service, you may need to define firewall rules for the subnets that are invoking your webhooks.
{: note}

| Region     | Alert Notification Source Subnets                                                                          |
|------------|------------------------------------------------------------------------------------------------------------|
| `US-SOUTH` | 150.239.180.0/25  \n 169.46.0.64/29  \n 169.46.39.48/28  \n 169.46.58.24/29  \n 169.47.115.192/28  \n 169.47.71.24/29  \n 169.48.214.64/29  \n 169.48.235.16/28  \n 169.60.151.168/29  \n 169.62.221.32/28  \n 174.36.68.96/27  \n 50.22.148.64/26  \n 52.116.222.192/27  \n 52.117.187.192/27  \n 52.118.158.0/25  \n 52.118.7.64/26  \n 67.228.207.64/26  \n 67.228.219.0/25 |
| `EU-DE`    | 149.81.151.128/27  \n 149.81.201.192/26  \n 149.81.77.72/29  \n 149.81.99.192/28  \n 158.177.44.192/26  \n 159.122.102.32/29  \n 161.156.1.224/27  \n 161.156.102.200/29  \n 161.156.69.144/28  \n 161.156.77.64/26  \n 169.50.36.64/27  \n 169.50.9.0/28    |
| `EU-GB`    | 141.125.136.32/27  \n 141.125.73.112/29  \n 141.125.73.80/28  \n 158.175.124.224/27  \n 158.175.98.200/29  \n 159.122.210.168/29  \n 159.8.144.168/29  \n 159.8.149.208/28  \n 159.8.162.0/26  \n 161.156.209.192/26  \n 5.10.120.32/27  |
| `JP-OSA`   | 163.68.67.128/28  \n 163.68.67.96/29  \n 163.68.79.32/27  \n 163.69.66.168/29  \n 163.69.67.112/28  \n 163.69.70.64/27  \n 163.73.67.176/29  \n 163.73.67.192/28  \n 163.73.69.96/27  |
| `JP-TOK`   | 128.168.75.32/28  \n 128.168.75.8/29  \n 128.168.98.0/27  \n 161.202.255.64/27  \n 165.192.84.8/29  \n 165.192.97.96/27  \n 169.56.11.208/28  \n 169.56.51.232/29  |
| `US-EAST`  | 169.47.20.160/27  \n 169.55.109.112/29  \n 169.55.122.192/28  \n 169.59.131.160/27  \n 169.59.146.192/26  \n 169.60.112.72/29  \n 169.60.82.240/28  \n 169.62.28.160/28  \n 169.62.3.80/29  \n 169.62.46.192/27  \n 52.116.95.64/26  \n 52.117.71.128/26  |
| `AU-SYD`   | 130.198.66.144/28  \n 130.198.80.152/29  \n 135.90.73.96/29  \n 135.90.78.192/28  \n 135.90.94.96/27  \n 168.1.115.192/27  \n 168.1.213.32/27  \n 168.1.213.72/29  \n 168.1.41.96/28  |
| `CA-TOR`   | 158.85.78.224/27  \n 158.85.94.128/29  \n 163.74.67.192/28  \n 163.74.69.184/29  \n 163.74.71.96/27  \n 163.75.65.232/29  \n 163.75.72.192/27  \n 169.55.129.208/28  |
| `BR-SAO` | 163.107.66.96/29  \n 163.107.68.128/28  \n 163.107.71.32/27  \n 163.109.67.240/29  \n 163.109.73.128/27  \n 169.57.141.40/29  \n 169.57.186.0/27  \n 169.57.195.0/28 |
{: caption="Source Subnets for Webhook notifications from {{site.data.keyword.sysdigsecure_full_notm}}" caption-side="top"}
