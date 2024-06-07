---

copyright:
  years:  2023
lastupdated: "2023-05-08"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Configuring {{site.data.keyword.registryshort_notm}} credentials (WIP)
{: #registry-ibm-cloud}

You can use {{site.data.keyword.sysdigsecure_short}} API tokens to authenticate with the {{site.data.keyword.sysdigsecure_full_notm}} service when you use Python scripts or the {{site.data.keyword.sysdigsecure_full_notm}} REST API to automate routine tasks and monitor notifications.
{: shortdesc}

Consider the following information for each instance of the {{site.data.keyword.sysdigsecure_full_notm}} service:

* There is a Monitor API token per team.
* If the token is compromised or your organization's security policies require resetting the token after certain conditions, a user with administration permissions can reset the API token.



1. Select the icon with your initials at the bottom left
2. In the *Secrets Management* section, select **Registry Credentials**.
3. Select **+Add Registry**
4. Enter the following data to configure the registry:

    Enter a name, e,g, `ibm_cloud_registry`. Notice that dashes are not allowed.

    Enter a path.

    Select a type. Choose **Docker V2**.

    Enter the username **iamapikey**.

    Enter the password.

    Enter the *Internal Registry Address*.

5. Enable *Allow self signed* to

6. Enable *Use Image to Test Credentials*


user = iamapikey   most likely

[Accessing container registry](https://cloud.ibm.com/docs/Registry?topic=Registry-registry_access)

```
iamapikey The password is an IAM API key that is used internally by the registry to generate an IAM access token. This type of authentication is the preferred type for automation. You can use a user API key or a service ID API key. For more information, see Accessing your namespaces in automation.
```



ICR is a Docker V2 compatible registry
