---

copyright:
  years:  2023, 2024
lastupdated: "2024-04-17"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Managing Secure API tokens
{: #secure_token}

You can use Secure API tokens to authenticate with the {{site.data.keyword.sysdigsecure_full}} service in REST API calls that you make to automate routine tasks and monitor notifications.
{: shortdesc}

Consider the following information for each instance of the {{site.data.keyword.sysdigsecure_short} service:

* There is a Secure API token per team.
* If the token is compromised or your organization's security policies require resetting the token after certain conditions, a user with administration permissions can reset the API token.

## Getting the Sysdig Secure API token through the Security UI
{: #secure_token_get}

Complete the following steps to get the Sysdig Secure API token :

1. From the *Selector* button in the navigation bar, choose **Settings**.
2. Select the *User Profile* option.
3. From the *Sysdig Secure API* section, copy the **Sysdig Secure API Token**.

After you get the token, you can run API calls and use this token in the `Authorization` header.

When you copy the token include the `Bearer` keyword: `Authorization: Bearer MONITOR_API_TOKEN`
{: note}

## Resetting the Sysdig Secure API token through the Security UI
{: #secure_token_reset}

Complete the following steps to reset the Sysdig Secure API token :

1. From the *Selector* button in the navigation bar, choose **Settings**.
2. Select the *User Profile* option.
3. In the *Sysdig Secure API* section, click **Reset Token** to reset the API token.

Remember to update the services and applications that use this token with the new value.
{: note}

## Getting the Sysdig Secure API token by using the API
{: #secure_token_get_api}

You can use the Token API to get the Sysdig Secure API token.

For example, you can use the following cURL command to get the Sysdig Secure API token :

```shell
curl -X GET <SECURITY_REST_API_ENDPOINT>/api/token -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "TeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

```text
GET <SECURITY_REST_API_ENDPOINT>/api/token -H "Authorization: $AUTH_TOKEN" -H "IBMInstanceID: $GUID" -H "TeamID: $TEAM_ID" -H "content-type: application/json"
```
{: codeblock}

Where

* `<SECURITY_REST_API_ENDPOINT>` indicates the endpoint that is targeted by the REST API call. For more information, see [REST API endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_rest_api). For example, the public endpoint for an instance that is available in us-south is `https://us-south.security-compliance-secure.cloud.ibm.com/api`.

* You can pass multiple headers by using `-H`.

    `Authorization` and `IBMInstanceID` are headers that are required for authentication.

    `TeamID` defines the team for which you want to get the Sysdig Secure API token.

    To get an `AUTH_TOKEN` and the `GUID` see, [Headers for IAM tokens](/docs/workload-protection?topic=workload-protection-using-curl#using-curl-headers-iam).

When the authorization that is allowed in an instance is set to `IAM_ONLY`, you get the following response `{"errors":[{"reason":"Not enough privileges to complete the action","message":"Access is denied"}]}` when you try to get the Sysdig Secure API token.
{: note}
