---

copyright:
  years: 2026
lastupdated: "2026-05-14"

keywords: cloud detection and response, CDR, ibm cloud, falco, rules, fields, activity tracker

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Reference Library for {{site.data.keyword.cloud_notm}} CDR Threat Detection Rules
{: #cdr-rules-reference}

{{site.data.keyword.sysdigsecure_short}} enables you to create and customize Threat Detection Rules to detect suspicious activity in your {{site.data.keyword.cloud_notm}} environments. This topic provides all the fields available for writing Falco rules against {{site.data.keyword.cloud_notm}} audit events ingested via CDR.
{: shortdesc}

Rules targeting {{site.data.keyword.cloud_notm}} audit events must use `source: ibm_activitytracker`. Fields can be accessed directly by their plugin name (e.g. `ibm.action`) or via the raw JSON path using `jevt.value[/fieldPath]` (for example `jevt.value[/action]`).
{: note}

## Fields
{: #cdr-rules-reference-fields}

In Threat Detection rules, a field represents one specific attribute the event captured from a raw event. You can use fields to define the detection condition and the output.

### Field Class: `ibm` (event)
{: #cdr-rules-reference-fields-ibm}

Top-level fields present in every {{site.data.keyword.cloud_notm}} audit event.

Event Sources: `ibm_activitytracker`

Name | Type | JSON path | Description
:----|:-----|:----------|:-----------
`ibm.action` | string | `/action` | The action that triggered the event. For example, `iam-am.policy.delete` or `iam-identity.user-apikey.create`.
`ibm.correlationId` | string | `/correlationId` | Unique GUID used to correlate related events across multiple services in the same account.
`ibm.dataEvent` | boolean | `/dataEvent` | Indicates whether the event is a data event (`true`) or a management event (`false`).
`ibm.eventTime` | string | `/eventTime` | Timestamp when the event was created, in ISO 8601 format.
`ibm.id` | string | `/id` | Optional field that can be used to correlate activity tracking events within a service.
`ibm.logSourceCRN` | string | `/logSourceCRN` | Cloud Resource Name (CRN) of the service instance that generated the event.
`ibm.message` | string | `/message` | Human-readable description of the event.
`ibm.observer.name` | string | `/observer/name` | Always set to `ActivityTracker`. Identifies the observer service that recorded the event.
`ibm.outcome` | string | `/outcome` | Result of the action. Typical values: `success`, `failure`, `pending`.
`ibm.requestData` | JSON | `/requestData` | Additional information about the request, when available.
`ibm.responseData` | JSON | `/responseData` | Additional information about the response, when available.
`ibm.saveServiceCopy` | boolean | `/saveServiceCopy` | When `true`, the service that generated the event saves a copy for IBM Cloud auditing.
`ibm.severity` | string | `/severity` | Level of threat the action may have on {{site.data.keyword.cloud_notm}}. Typical values: `normal`, `warning`, `critical`.

### Field Class: `ibm.initiator`
{: #cdr-rules-reference-fields-initiator}

Fields that describe the identity and origin of the entity that requested the action.

Event Sources: `ibm_activitytracker`

Name | Type | JSON path | Description
:----|:-----|:----------|:-----------
`ibm.initiator.id` | string | `/initiator/id` | ID of the initiator that requested the action. For users this is the IBMid; for service IDs this is the `ServiceId-xxx` value.
`ibm.initiator.name` | string | `/initiator/name` | Username or name of the initiator. When the initiator is an {{site.data.keyword.IBM_notm}} service, this field is set to `IBM` or the name of the service.
`ibm.initiator.authnId` | string | `/initiator/authnId` | ID of the user that logged in to {{site.data.keyword.cloud_notm}}.
`ibm.initiator.authnName` | string | `/initiator/authnName` | Username of the user that logged in to {{site.data.keyword.cloud_notm}}.
`ibm.initiator.typeURI` | string | `/initiator/typeURI` | Type of the event source. For example, `service/security/account/user` or `service/security/account/serviceid`.
`ibm.initiator.credential.type` | string | `/initiator/credential/type` | Type of credential used by the initiator. Typical values: `apikey`, `token`, `serviceid`.
`ibm.initiator.host.address` | string | `/initiator/host/address` | IP address or URL from which the request originated, such as the {{site.data.keyword.cloud_notm}} console or CLI.
`ibm.initiator.host.addressType` | string | `/initiator/host/addressType` | Type of IP address. For example, `IPv4` or `IPv6`.
`ibm.initiator.host.agent` | string | `/initiator/host/agent` | User-agent string identifying where the request originated, for example a CLI version or browser.

### Field Class: `ibm.target`
{: #cdr-rules-reference-fields-target}

Fields that describe the {{site.data.keyword.cloud_notm}} resource on which the action was executed.

Event Sources: `ibm_activitytracker`

Name | Type | JSON path | Description
:----|:-----|:----------|:-----------
`ibm.target.id` | string | `/target/id` | CRN or identifier of the {{site.data.keyword.cloud_notm}} resource on which the action was executed.
`ibm.target.name` | string | `/target/name` | Human-readable name of the {{site.data.keyword.cloud_notm}} resource on which the action was executed.
`ibm.target.alias` | string | `/target/alias` | Alias of the cloud resource used in the request, when applicable.
`ibm.target.typeURI` | string | `/target/typeURI` | Type of the target resource. For example, `iam-am/policy` or `iam-identity/account/serviceid`.
`ibm.target.resourceGroupId` | string | `/target/resourceGroupId` | CRN of the resource group associated with the target resource.
`ibm.target.host.address` | string | `/target/host/address` | IP address or URL of the target service.

### Field Class: `ibm.reason`
{: #cdr-rules-reference-fields-reason}

Fields that provide additional detail about the outcome of an action, particularly for failed requests.

Event Sources: `ibm_activitytracker`

Name | Type | JSON path | Description
:----|:-----|:----------|:-----------
`ibm.reason.reasonCode` | numeric | `/reason/reasonCode` | HTTP response code of the requested action. For example, `200` for success or `403` for unauthorized.
`ibm.reason.reasonType` | string | `/reason/reasonType` | Additional information about the result. For example, `OK` or `Forbidden`.
`ibm.reason.reasonForFailure` | string | `/reason/reasonForFailure` | Additional detail explaining why the action failed, when available.

## Rule writing examples
{: #cdr-rules-reference-fields-examples}

The following examples show how to reference these fields in Falco rules for CDR.

**Filtering by action and outcome:**

```yaml
condition: >
  jevt.value[/action] = "iam-am.policy.delete"
  and jevt.value[/outcome] = "success"
```
{: codeblock}

**Filtering by initiator credential type:**

```yaml
condition: >
  jevt.value[/action] startswith "iam-identity"
  and jevt.value[/initiator/credential/type] = "apikey"
```
{: codeblock}

**Filtering by source IP address:**

```yaml
condition: >
  jevt.value[/action] = "iam-identity.user-apikey.create"
  and not jevt.value[/initiator/host/address] in (trusted_ips)
```
{: codeblock}

For more information about creating rules and policies, see [Creating {{site.data.keyword.cloud_notm}} Threat Detection policy](/docs/workload-protection?topic=workload-protection-cdr-about#cdr-policy).
