---

copyright:
  years:  2023, 2026
lastupdated: "2026-07-01"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing access keys
{: #access_key}

An access key is a token that you must use to configure agents to successfully forward data to your {{site.data.keyword.sysdigsecure_short}} instance in {{site.data.keyword.cloud_notm}}.
{: shortdesc}


## Managing access keys by using the console
{: #access_key_ibm_cloud_ui}
{: ui}

You can view, create, disable, enable, and delete access keys for a {{site.data.keyword.sysdigsecure_short}} instance by using the {{site.data.keyword.cloud_notm}} console.

To manage access keys by using the console, complete the following steps:

1. In the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com){: external}, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Security > Compliance**.
2. Click the name of your {{site.data.keyword.sysdigsecure_short}} instance.
3. From the **Actions** menu, select **Manage key**.
4. Click **your dashboard** to view, create, disable, enable, or delete access keys. 

You can also hide the access key from non-administrators. For more information, go to [Non-admin users](https://docs.sysdig.com/en/administration/agent_access_key/#non-admin-users){: external}.
{: tip}

## Getting the access key by using the CLI
{: #access_key_cli}
{: cli}

To get the access key for a {{site.data.keyword.sysdigsecure_short}} instance by using the CLI, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. Log in to the region that contains your {{site.data.keyword.sysdigsecure_short}} instance by running the [`ibmcloud login`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) command:

    ```sh
    ibmcloud login
    ```
    {: pre}

3. Set the resource group where the instance is running by running the [`ibmcloud target`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target) command:

    ```sh
    ibmcloud target -g <resource_group>
    ```
    {: pre}

    Where `<resource_group>` is the name of the resource group. By default, the `default` resource group is set.

4. Get the instance name by running the [`ibmcloud resource service-instances`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instances) command:

    ```sh
    ibmcloud resource service-instances
    ```
    {: pre}

5. Get the name of the API key that is associated with the instance by running the [`ibmcloud resource service-keys`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_keys) command:

    ```sh
    ibmcloud resource service-keys --instance-name <instance_name> --output JSON
    ```
    {: pre}

    Where `<instance_name>` is the name of the instance that you obtained in the previous step.

    The output from this command includes the `Sysdig Access Key` field that contains the access key for the instance.

You can also create, delete, enable, or disable access keys by using the API or the console. To see the steps, switch to the API instructions, or go to [Managing access keys by using the console](/docs/workload-protection?topic=workload-protection-access_key&interface=ui#access_key_ibm_cloud_ui).
{: tip}

## Getting the access key by using the API
{: #access_key_get_api}
{: api}

You can get the access key by using the CLI or the console. To see the steps, switch to the CLI or UI instructions. You can also use the API to retrieve all available access keys. For more information, see [Viewing the available access keys by using the API](/docs/workload-protection?topic=workload-protection-access_key&interface=api#access_key_view).

## Creating an access key by using the API
{: #access_key_create}
{: api}

If the access key is compromised or you have a policy to renew it after a number of days, you can generate a new access key and disable the old one.

To create a new access key for an {{site.data.keyword.sysdigsecure_short}} instance, complete the following steps:

1. Copy the API token from the {{site.data.keyword.sysdigsecure_short}} UI. For more information, see [Retrieve the Sysdig API token](https://docs.sysdig.com/en/administration/retrieve-the-sysdig-api-token/){: external}.

2. Issue a curl POST request against the endpoint to generate a new access key:

    ```sh
    curl -X POST -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https://ENDPOINT/api/customer/accessKeys
    ```
    {: pre}

    Where:

    * `ENDPOINT` is the URL for the region where the instance is available. For more information, see [Endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints).
    * `SYSDIG_API_TOKEN` is the API token that you obtained in step 1.
    * `GUID` is the GUID of the instance that is associated with the access key.

    For example:

    ```sh
    curl -X POST -H 'Authorization: Bearer xxxxxxx' -H 'IBMInstanceID: 12345678-1234-1234-1234-123456789012' https://us-east.security-compliance-secure.cloud.ibm.com/api/customer/accessKeys
    ```
    {: pre}

    The output provides the generated access key in the response:

    ```json
    {
        "customerAccessKey": {
            "enabled": true,
            "accessKey": "12345678-1234-1234-1234-123456789012",
            "dateCreated": 1573852152224,
            "dateDisabled": null,
            "limit": null,
            "reservation": null,
            "teamId": null
        }
    }
    ```
    {: screen}

    You can now use the access key to configure agents.

## Disabling an access key by using the API
{: #access_key_disable}
{: api}

To disable an existing access key for an {{site.data.keyword.sysdigsecure_short}} instance, complete the following steps:

1. Copy the API token from the {{site.data.keyword.sysdigsecure_short}} UI. For more information, see [Retrieve the Sysdig API token](https://docs.sysdig.com/en/administration/retrieve-the-sysdig-api-token/){: external}.

2. Issue a curl POST request against the endpoint to disable the access key:

    ```sh
    curl -X POST -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https://ENDPOINT/api/customer/accessKeys/ACCESS_KEY/disable
    ```
    {: pre}

    Where:

    * `ENDPOINT` is the URL for the region where the instance is available. 
    * `SYSDIG_API_TOKEN` is the API token that you obtained in step 1.
    * `ACCESS_KEY` is the access key that you want to disable.
    * `GUID` is the GUID of the instance that is associated with the access key.

    After you disable the access key, agents that are connected with the access key are immediately blocked from sending metrics to this {{site.data.keyword.sysdigsecure_short}} instance.
    {: important}

    For example:

    ```sh
    curl -X POST -H 'Authorization: Bearer xxxxxxx' -H 'IBMInstanceID: 12345678-1234-1234-1234-123456789012' https://us-east.security-compliance-secure.cloud.ibm.com/api/customer/accessKeys/b302311f-aa1c-4930-8726-59fb4ba0fe84/disable
    ```
    {: pre}

    The output provides the disabled access key in the response:

    ```json
    {
        "customerAccessKey": {
            "enabled": false,
            "accessKey": "12345678-1234-1234-1234-123456789012",
            "dateCreated": 1573852152224,
            "dateDisabled": 1683550789329,
            "limit": null,
            "reservation": null,
            "teamId": null
        }
    }
    ```
    {: screen}


## Enabling an access key by using the API
{: #access_key_enable}
{: api}

To enable an existing access key for an {{site.data.keyword.sysdigsecure_short}} instance, complete the following steps:

1. Copy the API token from the {{site.data.keyword.sysdigsecure_short}} UI. For more information, see [Retrieve the Sysdig API token](https://docs.sysdig.com/en/administration/retrieve-the-sysdig-api-token/){: external}.

2. Issue a curl POST request against the endpoint to enable the access key:

    ```sh
    curl -X POST -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https://ENDPOINT/api/customer/accessKeys/ACCESS_KEY/enable
    ```
    {: pre}

    Where:

    * `ENDPOINT` is the URL for the region where the instance is available. 
    * `SYSDIG_API_TOKEN` is the API token that you obtained in step 1.
    * `ACCESS_KEY` is the access key that you want to enable.
    * `GUID` is the GUID of the instance that is associated with the access key.

After you enable the access key, you must manually restart the agents because an agent that connects with a disabled access key is terminated.
{: note}

## Viewing the available access keys by using the API
{: #access_key_view}
{: api}

To view all of the access keys for an {{site.data.keyword.sysdigsecure_short}} instance, complete the following steps:

1. Copy the API token from the {{site.data.keyword.sysdigsecure_short}} UI. For more information, see [Retrieve the Sysdig API token](https://docs.sysdig.com/en/administration/retrieve-the-sysdig-api-token/){: external}.

2. Issue a curl GET request against the regional endpoint to view the access keys:

    ```sh
    curl -X GET -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https://ENDPOINT/api/customer/accessKeys
    ```
    {: pre}

    Where:

    * `ENDPOINT` is the URL for the region where the instance is available. For more information, see [Endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints).
    * `SYSDIG_API_TOKEN` is the API token that you obtained in step 1.
    * `GUID` is the GUID of the instance that is associated with the access key.

    The output provides a list of the access keys and whether they are enabled:

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


## Deleting access keys by using the API
{: #access_key_delete}
{: api}

To delete an access key for an {{site.data.keyword.sysdigsecure_short}} instance, complete the following steps:

1. Copy the API token from the {{site.data.keyword.sysdigsecure_short}} UI. For more information, see [Retrieve the Sysdig API token](https://docs.sysdig.com/en/administration/retrieve-the-sysdig-api-token/){: external}.

2. Issue a curl `DELETE` request against the regional endpoint to delete the access key:

    ```sh
    curl -X DELETE -H 'Authorization: Bearer SYSDIG_API_TOKEN' -H 'IBMInstanceID: GUID' https://ENDPOINT/api/customer/accessKeys/ACCESS_KEY
    ```
    {: pre}

    Where:

    * `ENDPOINT` is the URL for the region where the instance is available. 
    * `SYSDIG_API_TOKEN` is the API token that you obtained in step 1.
    * `GUID` is the GUID of the instance that is associated with the access key.
    * `ACCESS_KEY` is the access key to be deleted. You can [view a list of all access keys](/docs/workload-protection?topic=workload-protection-access_key&interface=api#access_key_view) to obtain the access key values.
