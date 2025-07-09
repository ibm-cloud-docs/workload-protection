---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords: activity tracker for IBM Cloud Monitoring, IBM Cloud, audit, activity tracker, events, audit logs

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Auditing events
{: #at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the {{site.data.keyword.sysdigsecure_full}} service in {{site.data.keyword.cloud}}.
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
