---

copyright:
years: 2024
lastupdated: "2024-11-15"

keywords: workload protection, data portability, export

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.sysdigsecure_short}}
{: #data-portability}

Data portability involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer’s own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.Bluemix_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.

The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer’s application code, deployment automation, and so on.

The conversion of the exported data and configuration to the format that’s required by the alternative infrastructure and adapted applications.

For more information about your responsibilities for {{site.data.keyword.sysdigsecure_short}}, check otu [Shared responsibilities for {{site.data.keyword.sysdigsecure_short}}](/docs/workload-protection?topic=workload-protection-shared-responsibilities).

## Data export procedures
{: #data-portability-procedures}

{{site.data.keyword.sysdigsecure_short}} provides the mechanisms to export your content that’s uploaded, stored, and processed when you use the service.

For more information about how to get data from {{site.data.keyword.sysdigsecure_short}}, including supported data formats, check out the [API docs](/apidocs/workload-protection).
