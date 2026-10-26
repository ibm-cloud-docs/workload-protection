---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords: activity tracker, IBM Cloud, security events, audit logs, auditing, CADF, monitoring

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Auditing events
{: #at_events}

Use the Activity Tracker service to monitor user and application interactions with the {{site.data.keyword.sysdigsecure_full_notm}} service, track security events, and meet regulatory audit requirements.
{: shortdesc}

{{site.data.keyword.atracker_short}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-getting-started).

{{site.data.keyword.sysdigsecure_full_notm}} automatically generates events so that you can track activity on your service instance.


## Captures: List of management events
{: #at_events_captures}

| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-secure.capture.create`       | An event is created when you create a  capture |
| `sysdig-secure.capture.read`         | An event is created when you access a capture |
| `sysdig-secure.capture.list`       | An event is created when you list captures |
| `sysdig-secure.capture.update`       | An event is created when you update a capture |
| `sysdig-secure.capture.delete`       | An event is created when you delete a capture |
{: caption="Captures: List of activity tracker actions" caption-side="top"}


## Teams: List of management events
{: #at_events_teams}


| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-secure.team.create`          | An event is created when you create a team |
| `sysdig-secure.team.read`            | An event is created when you view a team definition |
| `sysdig-secure.team.list`            | An event is created when you list the definied teams |
| `sysdig-secure.team.update`          | An event is created when you update a team definition |
| `sysdig-secure.team.delete`          | An event is created when you delete a team |
{: caption="Teams: List of activity tracker actions" caption-side="top"}


## AccessKey: List of management events
{: #at_events_accesskey}


| Action                                | Description                                       |
|---------------------------------------|---------------------------------------------------|
| `sysdig-secure.accessKey.create`          | An event is created when you create an access key |
| `sysdig-secure.accessKey.list`            | An event is created when you view the access key |
| `sysdig-secure.accessKey.delete`          | An event is created when you delete an access key |
{: caption="AccessKey: List of activity tracker actions" caption-side="top"}

## Customer agreement: List of management events
{: #at_events_customer_agreement}

| Action                                   | Description                                           |
|------------------------------------------|-------------------------------------------------------|
| `sysdig-monitor.customer_agreement.read` | An event is created when a customer agreement is read |
{: caption="Customer agreement: List of activity tracker actions" caption-side="top"}

### Example: Customer agreement read event
{: #at_events_customer_agreement_example}

The following example shows an activity tracking event that is generated when {{site.data.keyword.IBM_notm}} support reads a customer agreement by using impersonation.

```json
{
  "action": "sysdig-monitor.customer_agreement.read",
  "correlationId": "00000000-0000-0000-0000-000000000000",
  "customerCRN": "crn:v1:bluemix:public:sysdig-monitor:us-south:a/{account_id}:{instance_id}::",
  "dataEvent": false,
  "eventTime": "2026-01-01T00:00:00.00+0000",
  "initiator": {
    "authnId": "{authn_id}",
    "authnName": "",
    "credential": {
      "type": "token"
    },
    "host": {
      "address": "",
      "agent": ""
    },
    "id": "{initiator_id}",
    "name": "",
    "typeURI": ""
  },
  "message": "IBM Cloud Monitoring: read customer_agreement",
  "observer": {
    "name": "ActivityTracker"
  },
  "outcome": "success",
  "reason": {
    "reasonCode": 200,
    "reasonType": "OK"
  },
  "requestData": {
    "impersonatedBy": "{support_user_id}",
    "isImpersonated": true,
    "payload": "",
    "queryParams": "",
    "requestURL": "/api/v1/customer/agreement",
    "teamId": 1,
    "teamName": "Monitor Operations"
  },
  "saveServiceCopy": true,
  "serviceName": "sysdig-monitor",
  "severity": "normal",
  "target": {
    "id": "crn:v1:bluemix:public:sysdig-monitor:us-south:a/{account_id}:{instance_id}:customer_agreement:",
    "name": "",
    "resourceGroupId": "crn:v1:bluemix:public:resource-controller::a/{account_id}::resource-group:{resource_group_id}",
    "typeURI": "sysdig-monitor/customer_agreement"
  }
}
```
{: codeblock}

The `requestData` fields:

`impersonatedBy`
:   The identity of the {{site.data.keyword.IBM_notm}} support user who performed the impersonated action.

`isImpersonated`
:   Set to `true` when the request is made by an {{site.data.keyword.IBM_notm}} support user on behalf of a customer.

`requestURL`
:   The API endpoint that was called during the impersonated session.

`teamId`
:   The numerical ID of the team context in which the impersonated action was performed.

`teamName`
:   The name of the team context in which the impersonated action was performed.


## Where to view the events
{: #ui}

The following table lists the {{site.data.keyword.cloud}} locations and the {{site.data.keyword.atracker_short}} instance location where you can find events:

| Instance location         | Location of events  |
|-----------------------------|---------------------|
| `Dallas (us-south)`         | `Dallas (us-south)` |
| `Washington (us-east)`      | `Washington (us-east)` |
| `Toronto (ca-tor)`          | `Toronto (ca-tor)` |
| `Sao Paulo (br-sao)`        | `Sao Paulo (br-sao)` |
| `Tokyo (jp-tok)`            | `Tokyo (jp-tok)` |
| `Osaka (jp-osa)`            | `Osaka (jp-osa)` |
| `Sydney (au-syd)`           | `Sydney (au-syd)` |
| `Frankfurt (eu-de)`         | `Frankfurt (eu-de)` |
| `London (eu-gb)`            | `London (eu-gb)` |
{: caption="Corresponding {{site.data.keyword.at_short}} instance and {{site.data.keyword.sysdigsecure_full_notm}} location." caption-side="top"}
