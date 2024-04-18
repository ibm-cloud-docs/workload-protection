---

copyright:
  years:  2023, 2024
lastupdated: "2024-04-18"

keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# CSPM APIs
{: #cspm-apis}

The {{site.data.keyword.sysdigsecure_full}} CSPM API can be used to generate remediation reports and create tasks.
{: shortdesc}

Consider the following when using the CSPM API:

* You must specify a zone in the request.  If a zone is not specified, the results are returned for policies applied to the default "Entire infrastructure" zone.

* Empty results are returned if no policy is applied to the "Entire infrastructure" zone.

* URL links to each control resource list API call are contained in the compliance results response.

For more information about the CSPM API, see the [{{site.data.keyword.sysdigsecure_full_notm}} API documentation](/apidocs/workload-protection#compliance-views).
