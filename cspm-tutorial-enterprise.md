---

copyright:
  years: 2026
lastupdated: "2026-06-16"

keywords: enterprise, compliance, cloud security posture management, app configuration

subcollection: workload-protection

content-type: tutorial
services: workload-protection, appconfig, openshift
account-plan: enterprise
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}

# Setting up {{site.data.keyword.sysdigsecure_short}} to scan an enterprise for compliance
{: #cspm-tutorial-enterprise}
{: toc-content-type="tutorial"}
{: toc-services="workload-protection, appconfig, openshift"}
{: toc-completion-time="2h"}

If you're an Administrator of an enterprise account, you can set up {{site.data.keyword.sysdigsecure_full}} to scan all of your enterprise's child accounts for compliance. By completing this tutorial, you learn how to set up your own instance of {{site.data.keyword.sysdigsecure_short}}, add an agent to a {{site.data.keyword.redhat_openshift_notm}} cluster to scan for vulnerabilities within that cluster, and set up {{site.data.keyword.appconfig_short}} so {{site.data.keyword.sysdigsecure_short}} can scan your enterprise account and all child accounts for compliance. 
{: shortdesc}

This topic focuses on enabling CSPM for {{site.data.keyword.cloud_notm}}. Need to enable CSPM for another cloud provider, like AWS, Azure, GCP, or OCI? See [Connect cloud accounts](https://docs.sysdig.com/en/sysdig-secure/connect-cloud-accounts/){: external} for more information.
{: tip}

Imagine that you're the administrator of an enterprise account that contains multiple child accounts. You want to set up {{site.data.keyword.sysdigsecure_short}} to scan your enterprise and all child accounts for compliance. You already have a running instance of {{site.data.keyword.appconfig_short}} in your enterprise account, and you want {{site.data.keyword.sysdigsecure_short}} to use that instance of {{site.data.keyword.appconfig_short}} to gather configuration information for compliance scanning. To keep your workloads as secure as possible, you also want to add an agent to your {{site.data.keyword.redhat_openshift_notm}} cluster so {{site.data.keyword.sysdigsecure_short}} can scan that cluster for threats and vulnerabilities.

## Before you begin
{: #prereqs}

Make sure that you're working in your enterprise account and that you have the necessary access.

* Make sure that you're working in your enterprise account by going to **Manage** > **Enterprise** in the {{site.data.keyword.cloud_notm}} console.
* Make sure that you have an instance of {{site.data.keyword.appconfig_short}} in your enterprise account.
* Make sure that you're assigned the following IAM roles:
   * Administrator of the Enterprise account.
   * Manager role or greater on the {{site.data.keyword.sysdigsecure_short}} service.
   * Manager role or greater on the {{site.data.keyword.appconfig_short}} service.

## Set up {{site.data.keyword.sysdigsecure_short}}
{: #setup-wp}
{: step}

Create an instance of {{site.data.keyword.sysdigsecure_short}} in your enterprise account.

You can use Terraform to set up an instance of {{site.data.keyword.sysdigsecure_short}} as code. For more information, see the [FAQ](/docs/workload-protection?topic=workload-protection-workload-protection-faq#faq-terraform-automation).
{: tip}

1. Go to the {{site.data.keyword.cloud_notm}} catalog, search for **Security and Compliance Center {{site.data.keyword.sysdigsecure_short}}**, and open the catalog listing for the service.
2. Select the location for your instance and select a plan that fits your needs.
3. Cloud security posture management (CSPM) is enabled by default, but you already have an instance of {{site.data.keyword.appconfig_short}} in your enterprise account, so you need to disable it.
    
    If you keep CSPM enabled, a new instance of {{site.data.keyword.appconfig_short}} is created to use with your instance of {{site.data.keyword.sysdigsecure_short}}. 
    {: important}

4. Accept the license agreements and click **Create**.
5. After the instance of {{site.data.keyword.sysdigsecure_short}} is created, copy the CRN for the instance and save it for later.

## Secure your cluster by connecting it to {{site.data.keyword.sysdigsecure_short}}
{: #secure-containers}
{: step}

In addition to compliance, {{site.data.keyword.sysdigsecure_short}} can also scan your containers and hosts to help keep them secure. To get this layer of protection, connect your container or host to {{site.data.keyword.sysdigsecure_short}} by adding an agent. This tutorial focuses on adding an agent to a {{site.data.keyword.redhat_openshift_notm}} cluster, but you can add an agent to many different containers and hosts, including Kubernetes clusters and {{site.data.keyword.powerSys_notm}} hosts.

1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Containers > Clusters** and click **Create cluster**.
2. Make sure that **{{site.data.keyword.redhat_openshift_notm}}** is selected as the orchestration platform. 
3. Customize your cluster by selecting the network and compute environment to run your cluster, the location of the cluster, along with the worker zones and subnets for the cluster. 
4. In the **Integrations** section, make sure {{site.data.keyword.sysdigsecure_short}} is enabled. Select **Existing {{site.data.keyword.sysdigsecure_short}} instance** as the configuration type, and select the instance of {{site.data.keyword.sysdigsecure_short}} that you just created from the **{{site.data.keyword.sysdigsecure_short}} instance** menu. 
5. Click **Create**.
    
    Do you already have a cluster? You can use the console to connect an existing {{site.data.keyword.redhat_openshift_notm}} or Kubernetes cluster to your instance of {{site.data.keyword.sysdigsecure_short}}. Go to **Containers** > **Clusters** to access the existing cluster. Then, click **Connect** in the {{site.data.keyword.sysdigsecure_short}} widget to connect your cluster to {{site.data.keyword.sysdigsecure_short}}.
    {: tip}

6. Wait 10-15 minutes then click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Security > Overview**. Select the {{site.data.keyword.sysdigsecure_short}} instance in the Vulnerabilities widget to view a snapshot of vulnerabilities within your cluster.

## Connect your {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.sysdigsecure_short}}
{: #connect-appconfig}
{: step}

So far, you set up {{site.data.keyword.sysdigsecure_short}} to scan a {{site.data.keyword.redhat_openshift_notm}} cluster for vulnerabilities. Next, establish trust between your {{site.data.keyword.sysdigsecure_short}} instance and the {{site.data.keyword.appconfig_short}} service, and connect your {{site.data.keyword.cloud_notm}} account to {{site.data.keyword.sysdigsecure_short}} to enable CSPM. Complete the following steps:

1. Create a trusted profile that allows your instance of {{site.data.keyword.sysdigsecure_short}} access to the {{site.data.keyword.appconfig_short}} service. Your {{site.data.keyword.sysdigsecure_short}} instance must already exist in your enterprise account. Complete the following steps:
    1. Go to **Manage** > **Access (IAM)** > **Trusted profiles** and click **Create**.
    2. Name the trusted profile `{{site.data.keyword.sysdigsecure_short}} access to {{site.data.keyword.appconfig_short}}`.
    3. Establish trust by selecting **{{site.data.keyword.cloud_notm}} services** as the trusted entity type, and enter the CRN for the {{site.data.keyword.sysdigsecure_short}} instance that you just created.
    4. Add the following access policies to the trusted profile:
        * Viewer and Usage Report Viewer roles on the Enterprise service.
        * Configuration Aggregator Reader and Manager roles on the {{site.data.keyword.appconfig_short}} service.
    5. After you create the trusted profile, copy the profile ID and save it for later.
2. Next, enable CSPM by connecting your instance of {{site.data.keyword.sysdigsecure_short}} to your {{site.data.keyword.cloud_notm}} account. Complete the following steps:
    1. Click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list** and search for `{{site.data.keyword.appconfig_short}}` to find your instance of {{site.data.keyword.appconfig_short}}.
    2. On the Getting started page of your {{site.data.keyword.appconfig_short}} instance, click **Details** and copy the CRN for the instance.
    3. Click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **>  Security > Compliance** and click the name of your {{site.data.keyword.sysdigsecure_short}} instance to open it.
    4. Go to **Sources** and click **Add** on the **{{site.data.keyword.cloud_notm}} Account** tab.
    5. Enter the trusted profile ID for `{{site.data.keyword.sysdigsecure_short}} access to {{site.data.keyword.appconfig_short}}` and the {{site.data.keyword.appconfig_short}} instance CRN and click **Add**.

When context-based restrictions are enabled for resources, configuration data cannot be collected unless access is provided. Create appropriate network zones and reference {{site.data.keyword.appconfig_short}} as the reference service to ensure {{site.data.keyword.sysdigsecure_short}} can scan your resources. For more information, see [Creating context-based restrictions](/docs/account?topic=account-context-restrictions-create&interface=ui).
{: important}

## Set up {{site.data.keyword.appconfig_short}} to collect configuration data from all child accounts 
{: #setup-appconfig}
{: step}

Your instance of {{site.data.keyword.sysdigsecure_short}} can now use the {{site.data.keyword.appconfig_short}} instance to scan your account and resources for compliance. However, to scan your entire enterprise, {{site.data.keyword.appconfig_short}} needs access to all of your enterprise's child accounts. Create a trusted profile template and assign it to your child accounts. Complete the following steps: 

1. Create a [trusted profile template](/docs/enterprise-management?topic=enterprise-management-tp-template-create&interface=ui) and name it `trusted profile template for child accounts`. Include the following access policies: 
    * Viewer and ConfigReader for All Account Management services. 
    * Reader, Viewer, and ConfigReader for All Identity and Access enabled services. 
2. After you create the trusted profile template, copy the template ID and save it for later. 
3. Assign the trusted profile template to your child accounts and account groups in the enterprise. 
4. Create another trusted profile to grant {{site.data.keyword.appconfig_short}} access to read the trusted profile template that you just created. Complete the following steps: 
    1. Go to **Manage > Access (IAM) > Trusted profiles** and click **Create**.
    2. Name the trusted profile `{{site.data.keyword.appconfig_short}} access to child accounts`.
    3. Establish trust by selecting **{{site.data.keyword.cloud_notm}} services** as the trusted entity type, and enter the CRN for your {{site.data.keyword.appconfig_short}} instance.
    3. Add the following access policies to the trusted profile:
        * Viewer role on the Enterprise service.
        * Template Administrator, Assignment Administrator, and Viewer roles for All IAM Account Management services. 
    4. After you create the trusted profile, copy the profile ID and save it for later.

## Set up configuration aggregator in your instance of {{site.data.keyword.appconfig_short}}
{: #setup-configaggregator}
{: step}

CSPM is now enabled, but {{site.data.keyword.appconfig_short}} isn't collecting configuration data just yet. Turn on the configuration aggregator by completing the following steps: 

1. Click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Resource list** and search for `{{site.data.keyword.appconfig_short}}`.
2. Click the name of the {{site.data.keyword.appconfig_short}} instance to open it, then, click **Configuration aggregator**.
3. Click **Define an aggregation** and specify which regions you want to collect configuration data from.
4. Enter your enterprise ID, the ID for `trusted profile template for child accounts`, and the ID for `{{site.data.keyword.appconfig_short}} access to child accounts` that you just created and click **Save**.
5. Turn on **Recording** to begin collecting configuration data in your accounts.
6. Wait 24 hours for initial scanning to complete, then, go to the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Security > Overview** to view a snapshot of your compliance data from {{site.data.keyword.sysdigsecure_short}}.
