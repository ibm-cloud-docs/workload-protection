---

copyright:
  years:  2023, 2026
lastupdated: "2026-09-21"

keywords:

subcollection: workload-protection

---

# {{site.data.keyword.cloud_notm}} Framework for Financial Services
{: #financial-services}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.cloud_notm}} Framework for Financial Services policy. The change log lists changes that were made, ordered by the version number.

When controls are edited, removed from, or added to this policy in a way that is not compatible with the current version, a new minor version is released. To take advantage of the changes in a new version, [link the new policy to your zone](https://docs.sysdig.com/en/sysdig-secure/manage_posture_policies/#link-the-policy-to-a-zone){: external}.

## Version 2.0
{: #version-2}

The following controls have been updated to {{site.data.keyword.cloud_notm}} Framework for Financial Services v2.0 compared to v1.1.

| Posture control                                                                                                                                                             | Associated requirement(s)                                   | Update                 |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|------------------------|
| Check whether an IBM Cloud Shell File Upload and File Download is enabled                                                                                                   | AC-14(a), AC-4, AC-6, SC-7(4)(a), SC-7(5), SC-7(a), SC-7(b) | This control was added |
| Check whether an IBM Cloud Shell is enabled                                                                                                                                 | SC-3, SC-6                                                  | This control was added |
| Check whether an IBM Cloud Shell Web Preview is enabled                                                                                                                     | SC-3, SC-6                                                  | This control was added |
| Check whether any Cloud Object Storage buckets used by Cloud Logs Event Routing are configured as cross-region                                                              | AU-9(a)                                                     | This control was added |
| Check whether Cloud Internet Services (CIS) has DDoS protection enabled                                                                                                     | AC-4, SC-3, SC-7(4)(a), SC-7(a), SC-7(b), SC-7(c)           | This control was added |
| Check whether Cloud Internet Services (CIS) has web application firewall enabled                                                                                            | AC-4, SC-3, SC-7(4)(a), SC-7(a), SC-7(b), SC-7(c)           | This control was added |
| Check whether Cloud Internet Services (CIS) is configured with at least TLS v1.2 for all inbound traffic                                                                    | AC-4, SC-3, SC-7(4)(a), SC-7(a), SC-7(b), SC-7(c)           | This control was added |
| Check whether Cloud Object Storage buckets have global GET permissions disabled via bucket policy                                                                           | AC-1(a), AC-2(d), AC-2(g), AC-3, AC-6                       | This control was added |
| Check whether Cloud Object Storage quota enforcement is off for buckets that are configured to use Cloud Logs Event Routing                                                 | AU-9(a)                                                     | This control was added |
| Check whether IBM Client VPN cipher is set as appropriate                                                                                                                   | SC-7(a)                                                     | This control was added |
| Check whether IBM Cloud File Storage is encrypted                                                                                                                           | SC-12(2), SC-12(3), SC-12                                   | This control was added |
| Check whether IBM Cloud Logs logs are encrypted at rest                                                                                                                     | AU-9(a)                                                     | This control was added |
| Check whether IBM VPN For VPC Connection IKE Policy encryption is set as appropriate                                                                                        | SC-7(a)                                                     | This control was added |
| Check whether IBM VPN For VPC Connection IPSEC Policy encryption is set as appropriate                                                                                      | SC-7(a)                                                     | This control was added |
| Check whether IBM VPN IKEv1 protocol is not be used                                                                                                                         | SC-7(a)                                                     | This control was added |
| Check whether Public Access to IBM Cloud File Storage is blocked                                                                                                            | AC-14(a), AC-4, AC-6, SC-7(4)(a), SC-7(5), SC-7(a), SC-7(b) | This control was added |
| Check whether the API key has an appropriate rotation period                                                                                                                | IA-5(g), SC-12(2), SC-12(3), SC-12, SC-28(1), SC-28         | This control was added |
| Check whether the API key has been used within an appropriate time period                                                                                                   | IA-5(g), SC-12(2), SC-12(3), SC-12, SC-28(1), SC-28         | This control was added |
| Ensure inbound traffic from the Internet allowing access from 0.0.0.0/0 to ports Telnet (23) or RSH (514) is restricted                                                     | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure inbound traffic from the Internet allowing access from 0.0.0.0/0 to ports Telnet (23) or RSH port (514) is restricted                                                | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure inbound traffic from the Internet from 0.0.0.0/0 ports DNS (53), POP3 (110), SMTP (25). DHCP (67, 68), SNMP (161, 162) is restricted                                 | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure inbound traffic from the Internet from 0.0.0.0/0 ports NetBIOS (139), SMB (445), FTP (21), TFTP (69) is restricted                                                   | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure inbound traffic from the Internet from 0.0.0.0/0 to port DNS (53) is restricted                                                                                      | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure inbound traffic from the Internet from 0.0.0.0/0 to port NetBIOS (139) is restricted                                                                                 | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure inbound traffic from the Internet from 0.0.0.0/0 to port RDP (3389) is restricted                                                                                    | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure inbound traffic from the Internet from 0.0.0.0/0 to ports PostgreSQL (5432), MySQL (3306), MSSQL (4333, 1433, 1434), OracleSQL (1521), MongoDB (27017) is restricted | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure inbound traffic from the Internet from 0.0.0.0/0 to ports RDP (3389), SSH (22), VNC (Listener: 5500, Server: 5900), RPC (135, 111) is restricted                     | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure no PowerVS network access groups allow ingress from 0.0.0.0/0 to port 22                                                                                             | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure no PowerVS security groups allow ingress from 0.0.0.0/0 to port 22                                                                                                   | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure no workspace security groups allow ingress from 0.0.0.0/0 to port 3389                                                                                               | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
| Ensure the default network access group (NAG) of every PowerVS workspace restricts all traffic                                                                              | AC-4, SC-3, SC-7(a), SC-7(b), SC-7(c)                       | This control was added |
{: caption="Summary of the changes for version v2.0 of the {{site.data.keyword.cloud_notm}} for Financial Services policy" caption-side="bottom"}

## Default parameters values based on {{site.data.keyword.cloud_notm}} Framework for Financial Services
{: #default-parameters}

The following {{site.data.keyword.sysdigsecure_full}} posture controls have default parameters based on the {{site.data.keyword.cloud_notm}} Framework for Financial Services:

| Control | Default parameter value |
|------------|-------------|
| Check whether App ID Cloud Directory lockout policy after # failed sign-in attempts | **5** |
| Check whether App ID Cloud Directory lockout period is set to # minutes | **30** |
| Check whether App ID access tokens are configured to expire after # minutes | **30** |
| Check whether sign out for active sessions is set to # seconds | **1800** |
| Check whether Hyper Protect Crypto Services encryption keys are rotated at least every # months| **12** |
| Check whether Secrets Manager user credentials are rotated at least every # days | **90** |
| Check whether VPN for VPC has a Diffie-Hellman group set to at least # | **14** |
| Check whether each Application Load Balancer for VPC is configured to use at least # zones | **3** |
| Check whether a Red Hat OpenShift cluster has at least # worker nodes across multiple zones | **3** |
| Check whether each Virtual Private Cloud is configured to use at least # zones | **3** |
| Check whether at least # instances of Transit Gateway have been created | **1** |
| Check whether VPN for VPC authentication is configured with a strong pre-shared key with a minimum length of # characters | **24** |
| Check whether at least # Virtual Private Cloud (VPC)s have been created | **1** |
| Check whether Virtual Servers for VPC instance has the minimum # interfaces | **1** |
| Check whether there are at least # instances of Direct Link in an account | **2** |
| Check whether Hyper Protect Crypto Services instance has at least # crypto units | **(2, 3)** |
| Checks whether Toolchain is configured only with the allowed integration tools | **['appconfig', 'artifactory', 'bitbucketgit', 'cloudobjectstorage', 'customtool', 'draservicebroker', 'eventnotifications', 'githubconsolidated', 'gitlab', 'hashicorpvault', 'hostedgit', 'keyprotect', 'pagerduty', 'pipeline', 'private_worker', 'saucelabs', 'secretsmanager', 'security_compliance', 'slack', 'sonarqube']** |
