---

copyright:
  years:  2023
lastupdated: "2023-04-14"

keywords: IBM Cloud, disaster recovery, ha, high availability, redundancy

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.sysdigsecure_full}} is a multi-tenant, regional service that is available in {{site.data.keyword.cloud_notm}}. You can use it to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions and compliance from source to run. {{site.data.keyword.sysdigsecure_short}} provides high availability and disaster recovery.
{: shortdesc}

## Availability zones
{: #ha-dr-locations}

An availability zone is a logically and physically isolated location within an {{site.data.keyword.cloud_notm}} region where your data is processed and hosted.

* An availability zone has independent power, cooling, and network infrastructures that are isolated from other zones to strengthen fault tolerance by avoiding single points of failure between zones.

* An availability zone offers high bandwidth and low inter-zone latency within a region.

A region (location) is a geographically and physically separate group of one or more availability zones with independent electrical and network infrastructures that are isolated from other regions.

* Regions are designed to remove shared single points of failure with other regions and avoid low inter-zone latency within the region.

* Each region has 3 different data centers (DC) for redundancy.

The following table lists the high-availability (HA) status for the regions (locations) where the {{site.data.keyword.sysdigsecure_full_notm}} service is available:

| Geographical area             | Region                   | HA Status |
|-----------------------|--------------------------|-----------|
| `Asia Pacific`        | `Sydney (au-syd)`        | `MZR`     |
| `Asia Pacific`        | `Tokyo (jp-tok)`         | `MZR`     |
| `Asia Pacific`        | `Osaka (jp-osa)`         | `MZR`     |
| `Europe`              | `Frankfurt (eu-de)`      | `MZR`     |
| `Europe`              | `London (eu-gb)`         | `MZR`     |
| `North America`       | `Dallas (us-south)`      | `MZR`     |
| `North America`       | `Washington (us-east)`   | `MZR`     |
| `North America`       | `Toronto (ca-tor)`       | `MZR`     |
| `South America`       | `Sao Paulo (br-sao)`     | `MZR`     |
{: caption="Table 1. List of locations where the service is available" caption-side="top"}

Where

* A *geographical area* is a physical area or larger political body that contains one or more regions.

* A *region* is a defined geographic territory.

    A region can be a specific postal code area, a town, a city, a state, a group of states, or even a group of countries.

    A region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

* `MZR` specifies a [multi-zone region.](/docs/overview?topic=overview-locations#mzr-table)


## Availability of an instance
{: #ha-dr-region}

When you provision an instance, you select the MZR (location) where the instance is created. The region determines where the data is processed and the data is hosted.

A multizone region (MZR) consists of 3 or more availability zones that are independent from each other to ensure that single failure events affect only a single zone.

By default, each instance consists of 3 zones: one primary zone and two secondary zones.

* Each zone is located in a different data center in the region.

* The data in your primary zone is automatically replicated to the secondary zones with low latency. You don't need to do anything to enable the replication.

* When the primary zone fails, a secondary zone is elected as the primary to prevent your service instance from being affected.

* If 2 zones fail at the same time, the service is down.

The MZR architecture offers automatic failover between 2 zones, and high availability for an instance within a region.


## Disaster recovery (DR) of the service in a region
{: #dr}

Disaster recovery is about surviving a catastrophic failure or loss of availability in a single location.

{{site.data.keyword.sysdigsecure_full_notm}} follows {{site.data.keyword.cloud_notm}} requirements for [planning and recovering from disaster events](/docs/overview?topic=overview-zero-downtime#disaster-recovery).

If a regional disaster occurs:

* The estimated recovery time for rebuilding the regional site and restoring the service at another location is 24 hours.

* You need to update the endpoints of applications and agents to point to the ingestion endpoint in the new location.

* You need to restore your custom resources from your backups.

Historical data might be lost during a disaster.
{: note}
