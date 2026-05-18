---

copyright:

  years: 2026
lastupdated: "2026-05-18"

keywords: error messages, errors, message ID

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.sysdigsecure_short}} error messages
{: #bxn-error-messages}

When you receive an error message from {{site.data.keyword.cloud_notm}} or {{site.data.keyword.sysdigsecure_short}}, you can use the message to find more information about how to resolve the problem.
{: shortdesc}

## Cannot verify credentials
{: #cannot-verify-credentials}

**Message**: Cannot verify credentials. 

You don't have [sufficient permissions](/docs/workload-protection?topic=workload-protection-iam) to run the command. 

## Failed to install the Helm chart
{: #helm-install-fail}

**Message**: Error: INSTALLATION FAILED: cluster unreachable: failed to refresh token: oauth2: cannot fetch token: 400 Bad Request.

Set your cluster context and try again. 

## Failed to install the agent 
{: #agent-install-fail}

**Message**: Error: context deadline exceeded

Run the following command, then try adding the Helm repository again: 

```sh
rm $HOME/Library/Preferences/helm/repositories.lock
```
{: pre}

## Failed to uninstall the agent
{: #agent-uninstall-fail}

**Message**: Error: uninstall: Release not loaded: sysdig-agent: release: not found.

Re-run the command and make sure the `ibm-observe` namespace is included: 

```sh
helm delete sysdig-agent -n ibm-observe
```
{: pre}

## Open ID error
{: #open-id-error}

**Message**: OPEN_ID_AUTHORIZATION_ERROR

For instructions to fix this problem, see [Why is my dashboard not loading or showing errors?](/docs/workload-protection?topic=workload-protection-ts-dashboard-loading)

## {{site.data.keyword.cloud_notm}} integration failure 
{: #cloud-integration-error}

**Messages**: 
* {{site.data.keyword.IBM_notm}} Token api call failed with error code '500'.
* Exception while getting {{site.data.keyword.IBM_notm}} {{site.data.keyword.appconfig_short}} Account Token.
* Failed to connect to database. 

For instructions to fix this problem, see [Why is my {{site.data.keyword.IBM_notm}} integration showing errors?](/docs/workload-protection?topic=workload-protection-troubleshoot-integration-errors)
