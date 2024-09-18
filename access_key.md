---

copyright:
  years:  2023, 2024
lastupdated: "2024-07-30"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing access keys
{: #access_key}

The **Access Key** is a token that you must use to configure agents to successfully forward data to your {{site.data.keyword.sysdigsecure_full}} instance in {{site.data.keyword.cloud_notm}}.
{: shortdesc}


## Getting the access key through the {{site.data.keyword.cloud_notm}} UI
{: #access_key_ibm_cloud_ui}

To get the access key for an {{site.data.keyword.sysdigsecure_full_notm}} instance through the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.

2. Go to the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) &gt; **Resource list**.

3. Select **Security**. You can see the list of instances that are available on {{site.data.keyword.cloud_notm}}.

4. Identify the instance for which you want to get the access key. Click the *Actions* icon ![Actions icon](../../icons/action-menu-icon.svg "Actions") next to the instance and then click **Manage key**.

    A window opens where you can click **Show key** to view the access key.



## Getting the access key through the CLI
{: #access_key_cli}

To get the access key for a instance through the command line, complete the following steps:

1. [Pre-requisite] [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. Log in to the region in the {{site.data.keyword.cloud_notm}} where the instance is running. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Set the resource group where the instance is running. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

4. Get the instance name. Run the following command: [ibmcloud resource service-instances](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instances)

    ```text
    ibmcloud resource service-instances
    ```
    {: pre}

5. Get the name of the API key that is associated with the instance. Run the [`ibmcloud resource service-keys`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_keys) command:

    ```text
    ibmcloud resource service-keys --instance-name INSTANCE_NAME  --output JSON
    ```
    {: pre}

    where INSTANCE_NAME is the name of the instance that you obtained in the previous step.

    The output from this command includes the field **Sysdig Access Key** that contains the access key for the instance.





## Creating an access key
{: #access_key_create}

If the access key is compromised or you have a policy to renew it after a number of days, you can generate a new access key and disable the old one.

To create a new access key for an {{site.data.keyword.sysdigsecure_full_notm}} instance, complete the following steps:

1. Obtain the {{site.data.keyword.sysdigsecure_short}} API token from the {{site.data.keyword.sysdigsecure_full_notm}} UI. [Learn more](/docs/workload-protection?topic=workload-protection-api_token#api_token_get).

2. Issue a curl POST request against the endpoint to generate a new access key.

    ```text
    curl -XPOST -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https:ENDPOINT/api/customer/accessKeys
    ```
    {: pre}

    Where

    * `ENDPOINT` is the URL for the region where the instance is available. For more information, see [Endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints).
    * `SYSDIG_API_TOKEN` is the API token that you get in step 1.
    * `GUID` is the GUID of the instance that is associated with the access key.

    For example, to create an access key, you can run the following:

    ```text
     curl -XPOST -H 'Authorization: Bearer xxxxxxx' https://us-east.security-compliance-secure.cloud.ibm.com/api/customer/accessKeys
    ```
    {: pre}

    The output will provide the newly generated access key in the response.

    ```json
    {"customerAccessKey":{"enabled":true,"accessKey":"b302311f-aa1c-4930-8726-59fb4ba0fe84","dateCreated":1683550580444,"dateDisabled":null,"limit":null,"reservation":null,"teamId":null}}
    {
        "customerAccessKey": {
            "enabled": true,
            "accessKey": "12345678-1234-1234-1234-123456789012",
            "dateCreated": 1573852152224,
            "dateDisabled": null,
            "limit":null,
            "reservation":null,
            "teamId":null
        }
    }
    ```
    {: screen}

3. The access key can now be used in the agent configuration files.

## Disabling an access key
{: #access_key_disable}

To disable an existing access key for an {{site.data.keyword.sysdigsecure_full_notm}} instance, complete the following steps:

1. Obtain the API Token from the {{site.data.keyword.sysdigsecure_full_notm}} UI ( [see instructions](/docs/workload-protection?topic=workload-protection-api_token#api_token_get) ).

2. Issue a curl POST request against the endpoint to disable the given access key.

    ```text
    curl -XPOST -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https:ENDPOINT/api/customer/accessKeys/ACCESS_KEY/disable
    ```
    {: pre}

    Where

    * `ENDPOINT` is the URL for the region where the instance is available. For more information, see [Endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints).
    * `SYSDIG_API_TOKEN` is the API Token retrieved in step 1.
    * `ACCESS_KEY` is the access key that you wish to disable.
    * `GUID` is the GUID of the instance that is associated with the access key.

    Once you disable the access key, the agents connected with the access key will be immeditely blocked from sending metrics to this {{site.data.keyword.sysdigsecure_full_notm}} instance.
    {: important}

    For example, to delete an access key, you can run the following:

    ```text
     curl -XPOST -H 'Authorization: Bearer xxxxxxx' https://us-east.security-compliance-secure.cloud.ibm.com/api/customer/accessKeys/<ACCESSKEY>/disable
    ```
    {: pre}

    The output will provide the newly generated access key in the response.

    ```json
    {"customerAccessKey":{"enabled":true,"accessKey":"b302311f-aa1c-4930-8726-59fb4ba0fe84","dateCreated":1683550580444,"dateDisabled":null,"limit":null,"reservation":null,"teamId":null}}
    {
        "customerAccessKey": {
            "enabled": false,
            "accessKey": "12345678-1234-1234-1234-123456789012",
            "dateCreated": 1573852152224,
            "dateDisabled":1683550789329,
            "limit":null,
            "reservation":null,
            "teamId":null
        }
    }
    ```
    {: screen}


## Enabling an access key
{: #access_key_enable}

To enable an existing access key for an {{site.data.keyword.sysdigsecure_full_notm}} instance, complete the following steps:

1. Obtain the API Token from the {{site.data.keyword.sysdigsecure_full_notm}} UI. [Learn more](/docs/workload-protection?topic=workload-protection-api_token#api_token_get).

2. Issue a curl POST request against the endpoint to enable the given access key.

    ```text
    curl -XPOST -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https://ENDPOINT/api/customer/accessKeys/ACCESS_KEY/enable
    ```
    {: pre}

    Where

    * `ENDPOINT` is the URL for the region where the instance is available. For more information, see [Endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints).
    * `SYSDIG_API_TOKEN` is the API Token retrieved in step 1.
    * `ACCESS_KEY` is the access key that you wish to enable.
    * `GUID` is the GUID of the instance that is associated with the access key.


After you enable the access key, the agents will need to be manually restarted since an agent that connects with a disabled access key will be terminated.
{: note}

## Viewing the available access keys
{: #access_key_view}

To view all of the access keys for an {{site.data.keyword.sysdigsecure_full_notm}} instance, complete the following steps:

1. Obtain the API Token from the {{site.data.keyword.sysdigsecure_full_notm}} UI. [Learn more](/docs/workload-protection?topic=workload-protection-api_token#api_token_get).

2. Issue a curl GET request against the regional endpoint to enable the given access key.

    ```text
    curl -XGET -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https://ENDPOINT/api/customer/accessKeys
    ```
    {: pre}

    Where

    * `ENDPOINT` is the URL for the region where the monitoring instance is available. For more information, see [Endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints).
    * `SYSDIG_API_TOKEN` is the API Token retrieved in Step 1.
    * `GUID` is the GUID of the instance that is associated with the access key.

    The output will provide a list of the access keys in the response and whether they are enabled.

    ```json
    {
        "customerAccessKeys": [
            {
                "enabled": true,
                "accessKey": "12345678-1234-1234-1234-123456789012",
                "dateCreated": 1541096409000,
                "dateDisabled": null,
                "limit": null,
                "reservation": null,
                "teamId": null
            },
            {
                "enabled": false,
                "accessKey": "87654321-1234-1234-1234-123456789012",
                "dateCreated": 1573849361000,
                "dateDisabled": 1573849367000,
                "limit": null,
                "reservation": null,
                "teamId": null
            }
        ]
    }
    ```
    {: screen}


## Deleting access keys
{: #access_key_delete}

To delete an access keys for an {{site.data.keyword.sysdigsecure_full_notm}} instance, complete the following steps:

1. Obtain the API Token from the {{site.data.keyword.sysdigsecure_full_notm}} UI. [Learn more](/docs/workload-protection?topic=workload-protection-api_token#api_token_get).

2. Issue a curl DELETE request against the regional endpoint to delete the access key.

    ```text
    curl -X DELETE -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https://ENDPOINT/api/customer/accessKeys/ACCESS_KEY
    ```
    {: pre}

    Where

    * `ENDPOINT` is the URL for the region where the monitoring instance is available. For more information, see [Endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints).
    * `SYSDIG_API_TOKEN` is the API Token retrieved in Step 1.
    * `GUID` is the GUID of the instance that is associated with the access key.
    * `ACCESS_KEY` is the access key to be deleted.  You can [view a list of all access keys](#access_key_view) to obtain the access key values.
    * `GUID` is the GUID of the instance that is associated with the access key.



## Hide the access key
{: #access_key_hide}


To hide the *Access Key* page for non-admin users in an {{site.data.keyword.sysdigsecure_short}} instance through the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.

2. Go to the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) &gt; **Resource list**.

3. Select **Security**. You can see the list of instances that are available on {{site.data.keyword.cloud_notm}}.

4. Identify the instance. Select **Open dashboard**.

5. From the *Selector* button in the navigation bar, choose **Settings** &gt; **User Profile** &gt; **Admin Priviledges**.

6. Enable the option **Hide Agent Install** to hide the access key for non-admin users.