---

copyright:
  years:  2023, 2025
lastupdated: "2025"

keywords:

subcollection: workload-protection

---

# {{site.data.keyword.cloud_notm}} Framework for Financial Services
{: #financial-services}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.cloud_notm}} Framework for Financial Services policy. The change log lists changes that were made, ordered by the version number.

When controls are edited, removed from, or added to this policy in a way that is not compatible with the current version, a new minor version is released. To take advantage of the changes in a new version, [assign the new policy to your zone](/docs/workload-protection?topic=workload-protection-posture-link-policy-to-zone).

## Version 2.0
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

