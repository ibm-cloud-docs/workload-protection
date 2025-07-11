---

copyright:
  years:  2023
lastupdated: "2023-12-13"
keywords:

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Protecting {{site.data.keyword.sysdigsecure_full}} resources with context-based restrictions
{: #cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to {{site.data.keyword.sysdigsecure_full}} resources can be controlled with context-based restrictions and identity and access management (IAM) policies.
{: shortdesc}

These restrictions work with traditional IAM policies, which are based on identity, to provide an extra layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure. Since both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. For more information, see [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis).

A user must have the Administrator role on the {{site.data.keyword.sysdigsecure_full}} service to create, update, or delete rules. A user must also have either the Editor or Administrator role on the Context-based restrictions service to create, update, or delete network zones. A user with the Viewer role on the Context-based restrictions service can only add network zones to a rule.
{: note}

Any {{site.data.keyword.sysdigsecure_full}} or audit log events generated come from the context-based restrictions service, not {{site.data.keyword.sysdigsecure_full}}. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor).

To get started protecting your {{site.data.keyword.sysdigsecure_full}} resources with context-based restrictions, see the tutorial for [Leveraging context-based restrictions to secure your resources](/docs/account?topic=account-context-restrictions-tutorial).

## Restrictions
{: #cbr-restrictions}

Consider the following when configuring context-based restrictions:

* Context-based restrictions do not affect connectivity of {{site.data.keyword.sysdigsecure_full}} agents since they do not use {{site.data.keyword.iamlong}}.

* Private connections between agents and {{site.data.keyword.sysdigsecure_full}} can be configured using [private service endpoints](/docs/monitoring?topic=monitoring-endpoints).
