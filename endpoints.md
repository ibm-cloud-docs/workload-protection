---

copyright:
  years:  2023
lastupdated: "2023-04-14"

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
| `US-EAST`   | `https://us-east.security-compliance-secure.cloud.ibm.com`       | 169.60.112.74  \n 169.55.109.114  \n 169.62.3.82        | https (TLS) 443 |
{: caption="Table 1. List of endpoints" caption-side="top"}




## REST API endpoints
{: #endpoints_rest_api}

To make API calls, you might need to define a firewall rule in your host.
{: note}

### Private REST API endpoints
{: #endpoints_rest_api_private}

| Region      | Private REST API endpoint                                     |
|-------------|---------------------------------------------------------------|
| `US-EAST`   | `https://private.us-east.security-compliance-secure.cloud.ibm.com/api`       |
{: caption="Table 2. Private REST API endpoints for the {{site.data.keyword.sysdigsecure_full_notm}} service" caption-side="top"}


### Public REST API endpoints
{: #endpoints_rest_api_public}


| Region      | Public REST API endpoint                                      |
|-------------|---------------------------------------------------------------|
| `US-EAST`   | `https://us-east.security-compliance-secure.cloud.ibm.com/api`       |
{: caption="Table 3. Public REST API endpoints for the {{site.data.keyword.sysdigsecure_full_notm}} service" caption-side="top"}




## Collector endpoints
{: #endpoints_ingestion}

Collector endpoints are ingestion endpoints that you can use to send data.


### Private Collector endpoints
{: #endpoints_ingestion_private}

To send metrics by using a private endpoint, you must [enable virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint) for your account.
{: note}

The following table lists the *Private Collector endpoints* that are available for each region:

| Region      | Private ingestion endpoint       | Private IP addresses       | {{site.data.keyword.sysdigsecure_full_notm}} agent ports   |
|-------------|----------------------------------|----------------------------|-----------|
| `US-EAST`   | `ingest.private.us-east.security-compliance-secure.cloud.ibm.com`    | 166.9.22.50  \n 166.9.24.43  \n 166.9.20.53      | TCP 6443  |
{: caption="Table 4. List of ingestion endpoints and private IP addresses to send data to the {{site.data.keyword.sysdigsecure_full_notm}}" caption-side="top"}


### Public Collector endpoints
{: #endpoints_ingestion_public}

The following table lists the *Public Collector endpoints* that are available for each region:

| Region      | Public ingestion endpoint      | Public IP addresses    | {{site.data.keyword.sysdigsecure_full_notm}} agent ports   |
|-------------|-------------------------------|-------------------------|---------|
| `US-EAST`   | `ingest.us-east.security-compliance-secure.cloud.ibm.com`           | 169.60.112.74  \n 169.55.109.114  \n 169.62.3.82      | TCP 6443 |
{: caption="Table 5. List of ingestion endpoints and public IP addresses to send data to the {{site.data.keyword.sysdigsecure_full_notm}}" caption-side="top"}


## Subnets for webhook notifications from {{site.data.keyword.sysdigsecure_full_notm}}
{: #endpoints_network_alert_subnets}

To receive alert notifications by using webhooks from the {{site.data.keyword.sysdigsecure_full_notm}} service, you may need to define firewall rules for the subnets that are invoking your webhooks.
{: note}

| Region     | Alert Notification Source Subnets                                                                          |
|------------|------------------------------------------------------------------------------------------------------------|
| `US-EAST`  | 169.47.20.160/27  \n 169.55.109.112/29  \n 169.55.122.192/28  \n 169.59.131.160/27  \n 169.59.146.192/26  \n 169.60.112.72/29  \n 169.60.82.240/28  \n 169.62.28.160/28  \n 169.62.3.80/29  \n 169.62.46.192/27  \n 52.116.95.64/26  \n 52.117.71.128/26  |
{: caption="Table 6. Source Subnets for Webhook notifications from {{site.data.keyword.sysdigsecure_full_notm}}" caption-side="top"}
