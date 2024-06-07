---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords: IBM Cloud, monitoring, alerts

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Working with alerts
{: #alerts}

In the {{site.data.keyword.sysdigsecure_full}} service, you can configure single alerts and multi-condition alerts to notify about problems that may require attention. When an alert is triggered, you can be notified through 1 or more notification channels. An alert definition can generate multi-channel notifications.
{: shortdesc}

An alert is a notification event that you can use to warn about situations that require attention. Each alert has a severity status. This status informs you about the criticality of the information it reports on.

When you define an alert, you must define the condition that triggers the notification, and one or more notification channels through which you want to be notified. You must also define the severity of the alert, and the type of alert. For more information about how to configure an alert, see [Configuring an alert](/docs/workload-protection?topic=workload-protection-config).

By default, severity is set to *warning*. You can set the severity of an alert to any of the following values: *emergency*, *alert*, *critical*, *error*, *warning*, *notice*, *informational*, *debug*

You can define an alert on a single metric or a set of metrics to notify of events or issues that you want to monitor.
- You can define a single condition alert.
- You can define a multi-condition alert. The alert threshold is configured by using complex conditions.
- You can define how the data is aggregated.
- You can use boolean logic to define alerts that report on multiple metrics.
- You get a notification when the alert condition is met.
- You can configure multiple notification channels per alert.
- Alerts are executed in 1 minute or less from receipt, with the option to configure the trigger wait time by hour or day.
- For PromQL alerts only, you can optionally configure a 0 minute wait time.


You can enable predefined alerts, modify alerts, and create custom alerts in the web UI and by using the {{site.data.keyword.sysdigsecure_full_notm}} API.

You manage alerts in the *Alerts* view of the web UI. You can configure the table columns that are displayed in the *Alerts* view. Valid column options are *Name*, *Scope*, *Alert When*, *Segment By*, *Notifications*, *Enabled*, *Modified*, *Captures*, *Channels*, *Created*, *Description*, *Email recipients*, *For at least*, *OpsGenie*, *PagerDuty*, *Severity*, *Slack*, *WebHook*, *SNS topics*, *Type*, and *VictorOps*.

## Types of alerts
{: #alerts_types}

The {{site.data.keyword.sysdigsecure_full_notm}} service includes pre-defined alerts that you can enable. In addition, you can configure custom alerts from panels in a dashboard, by using the REST API, or in the *Alerts* section of the web UI.

In the {{site.data.keyword.sysdigsecure_full_notm}} service, you can define any of the following types of alerts:

- Downtime: Use this type of alert to monitor sources and alert when they are down, for example, a bare metal.

- Metric: Use this type of alert to monitor time-series metrics and alert when they reach the thresholds defined.

- PromQL: Use this type of metric to monitor metrics by using a PromQL query.

- Event: Use this type of alert to monitor occurrences of specific events and alert when they reach the thresholds defined. For example, you can use this alert to monitor when a number of unauthorize access requests are reported.

- Anomaly Detection: Use this type of alert to monitor hosts based on historical behaviors and alert when they deviate from the expected pattern.

- Group Outlier: Use this type of alert to monitor hosts and be notified when 1 acts differently from the rest.


## Notification channels
{: #alerts_types_channels}

A notification channel defines where you want to receive information when an alert is triggered.

When you configure an alert, you can specify 1 or more notification channels.
{: note}

By default, when an alert is triggered, you get a notification in the *Events* section.

You can configure any of the following notification channels:
- Amazon SNS Topic
- Email
- IBM Cloud Functions
- IBM Event Notifications
- Microsoft Teams
- OpsGenie
- PagerDuty
- Slack
- Teams Email
- VictorOps
- WebHook
