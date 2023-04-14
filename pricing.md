---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}


# Pricing
{: #pricing_plans}

Different service plans are available for {{site.data.keyword.sysdigsecure_full_notm}}.
{: shortdesc}

The following service plans are available:

| Plans                                      | Plan ID                                | Plan Name                   |
|--------------------------------------------|----------------------------------------|-----------------------------|
| `Free Trial`                               | `0eae605c-7258-4bb7-8cb7-a4b96d5c94c3` | `lite`                      |
| `Graduated tier`                           | `00497f9a-f093-436b-98d7-c81845399516` | `graduated-tier`            |
{: caption="Table 1. Service plans" caption-side="top"}

A `Free Trial` {{site.data.keyword.sysdigsecure_full_notm}} instance expires after 30 days. In a `Graduated tier` plan, data is accessible and retained for 90 days.

## Estimating your cost
{: #price_estimate}

Cost is $0.07639 for each node hour.

To estimate your approximate cost, use the following formula.

```text
Number of agents x hours the agents run in a day x the number of days in a month x $0.07639
```
{: codeblock}

For example, if you are running one agent for 24 hours a day and the month has 30 days, the estimated cost is approximately $55.

```text
1 x 24 x 30 x $0.07639
```
{: codeblock}
