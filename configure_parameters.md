---

copyright:
  years: 2026
lastupdated: "2026-10-30"

keywords: posture controls, control parameters, compliance, configuration

subcollection: workload-protection

---

{{site.data.keyword.attribute-definition-list}}

# Configuring {{site.data.keyword.sysdigsecure_short}} control parameters
{: #cspm-configure-control}

Learn how to update {{site.data.keyword.sysdigsecure_full}} posture control parameters, understand where parameter values apply, and review best practices for customizing parameter values.
{: shortdesc}

Many {{site.data.keyword.sysdigsecure_short}} posture controls use configurable parameters to evaluate compliance. These parameters allow organizations to define approved locations, IP addresses, registries, credential rotation periods, encryption settings, and other control-specific requirements. The {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy relies on configurable posture control parameters to evaluate compliance. This guide focuses on the parameters associated with the policy and how to configure them to align compliance assessments with your organization's security and regulatory requirements.

Parameter values are configured directly on the posture control and are applied across the entire {{site.data.keyword.sysdigsecure_short}} instance.

## Setting parameter values
{: #set-parameter-values}

To customize parameter values:

1. In the {{site.data.keyword.cloud_notm}} console, click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg) **> Security > Compliance** then select your instance of {{site.data.keyword.sysdigsecure_short}}.
1. Click **Open dashboard**.

From there, you can access your policies and posture controls. For more information, see [Navigate Posture Controls List](https://docs.sysdig.com/en/sysdig-secure/posture_controls/#navigate-posture-controls-list){: external}.

## Control parameter scope
{: #parameter-scope}

Parameter values are stored on the control for your entire {{site.data.keyword.sysdigsecure_short}} instance. They are not stored inside an individual policy. Every policy that includes the same control uses the same parameter value.

You do not need to copy a policy to change a parameter value. You cannot specify different parameter values for the same control across different policies.

## Parameter input types
{: #parameter-input-types}

The UI supports two types of input fields for parameters:

| UI input type | How to enter values | Received value |
| --- | --- | --- |
| **List (chips)** (used by all list parameters) | Enter one value and press **Enter** or **Tab**. This action creates one chip. Repeat for each value. | A list with one item per chip. |
| **Number box** (used by all numeric parameters) | Enter a whole number. | A number. |
{: caption="Parameter input types" caption-side="bottom"}

Important considerations:

- List fields do not automatically split on commas. If you enter `eu-de, eu-gb` and press **Enter**, a single chip is created with the string `eu-de, eu-gb`. Some controls require this comma-separated format in a single chip ([Family P2](#cspm-parameter-family-p2)), but most list parameters require one chip per value.
- In numeric fields, `0` resets the value to the default. Entering `0` submits an empty value, which removes your custom value and restores the default. You cannot set `0` as an explicit custom value when the default is non-zero.

## Rules for configuring parameters
{: #five-rules}

Review the following rules to avoid common configuration errors:

Rule 1: Use one chip per value, except for CBR IP controls.
:   Most list parameters require one chip per region, IP address, resource name, or algorithm. The exceptions are the 32 CBR controls in [Family P2](#cspm-parameter-family-p2) and the second entry of the seven controls in [Family P3](#cspm-parameter-family-p3). For those controls, enter all IP addresses in one chip separated by commas. If you split them into multiple chips, only the first chip is evaluated and the control fails.

Rule 2: Most IP lists are evaluated as exact string matches, not ranges.
:   In families P2, P3, and P5, a CIDR block such as `10.0.0.0/16` does not cover `10.0.1.0/24` or `10.0.0.5`. Every IP address or CIDR block configured in {{site.data.keyword.cloud_notm}} must appear in the parameter exactly as configured. Only the three controls in [Family P6](#cspm-parameter-family-p6) evaluate whether an address falls inside a range.

Rule 3: Location values must match what the resource reports.
:   Different {{site.data.keyword.cloud_notm}} resources report their location at different levels: region (`eu-de`), zone (`eu-de-1`), data center (for {{site.data.keyword.powerSys_notm}}, such as `dal10`), or `global`. The allowed region parameter must contain every format that your resources use ([Family P1](#cspm-parameter-family-p1)).

Rule 4: Review default parameter behavior.
:   Some default settings cause a control to fail for every resource until you specify custom values (such as *Approved Registries*, *{{site.data.keyword.secrets-manager_short}} user credentials rotated at least every # days*, or *{{site.data.keyword.appid_short}} access tokens expire within # minutes*). Other defaults cause a control to always pass (such as controls that require at least a specified number of zones when the default is 0). The Default effect column in [Appendix A](#appendix-parameterized-controls) shows this for every control.


Rule 5: Resource names must match exactly.
:   Exclusion lists and IAM lists compare the resource name exactly as {{site.data.keyword.cloud_notm}} reports it, including case sensitivity. For container images, enter the image name rather than the image ID.

To find the exact value that {{site.data.keyword.sysdigsecure_short}} evaluates, open a failing finding and review the resource configuration in the resource panel or in **Inventory**. The value that the control compares (such as location, IP list, name, or cipher) is displayed exactly as {{site.data.keyword.sysdigsecure_short}} received it from {{site.data.keyword.cloud_notm}}. You can copy that value directly into the parameter.
{: tip}

## Parameter guide by control family
{: #parameter-family}

### P1: Allowed regions and locations
{: #cspm-parameter-family-p1}

Controls
:   *Check whether IBM `<resource type>` is provisioned in allowed region*. There is one control per resource type, plus *Check whether IBM resources are provisioned in allowed region*, which applies to every resource type. These controls are available in the Controls Library and are included in the {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy under requirements SC-7(a), SC-7(5), and CM-7(a).

UI label
:   `Allowed Region/Location where IBM Resource can be deployed`. Input type: list (chips).

The resource location must match one of the values in the list. Resources that report an empty location always pass. With an empty list, the control always passes.

Every location where your resources can run, with one chip per location, in every format that your resources report:

| Form | Example | Typical resources |
| --- | --- | --- |
| Region | `eu-de`, `eu-gb` | Most regional services ({{site.data.keyword.logs_full_notm}}, {{site.data.keyword.secrets-manager_short}}, {{site.data.keyword.keymanagementserviceshort}} keys, {{site.data.keyword.codeengineshort}}, {{site.data.keyword.vpn_vpc_short}}, and others) |
| Zone | `eu-de-1`, `eu-de-2`, `eu-de-3` | Some {{site.data.keyword.vpc_short}} resources |
| Data center | `dal10`, `lon04` | {{site.data.keyword.powerSys_notm}} resources (reported as workspace data center) |
| `global` | `global` | Global services and account-level resources (such as service IDs, {{site.data.keyword.atracker_short}} routes, and {{site.data.keyword.cis_short_notm}} zones) |
{: caption="Location formats for allowed regions parameters" caption-side="bottom"}

Use the following information to find the values in {{site.data.keyword.cloud_notm}}:

Regions
:   Run `ibmcloud regions` or check the Location column on the Resource list in the console.

Zones
:   Run `ibmcloud is zones <region>` (for example, `ibmcloud is zones eu-de`).

{{site.data.keyword.powerSys_notm}}
:   Check the workspace location by running `ibmcloud pi workspace list` or viewing **{{site.data.keyword.powerSys_notm}}** > **Workspaces**.

Format
:   One location per chip in lowercase, matching command output.

Parameter values are set per control. You must configure the list on each control that you evaluate. Add `global` only if you permit global resources. Without `global`, resources reporting a global location fail evaluation.

#### Allowed regions and locations examples
{: #p1examples}

The following examples show how to enter values for the allowed regions and locations parameter. Enter each value as a separate chip.

Frankfurt only, including global services
:   Enter the following values, one per chip:

    * `eu-de`
    * `eu-de-1`
    * `eu-de-2`
    * `eu-de-3`
    * `global`

Frankfurt and London
:   Enter the following values, one per chip:

    * `eu-de`
    * `eu-de-1`
    * `eu-de-2`
    * `eu-de-3`
    * `eu-gb`
    * `eu-gb-1`
    * `eu-gb-2`
    * `eu-gb-3`
    * `global`

Incorrect
:   `eu-de, eu-gb` in one chip. This is evaluated as a single string `eu-de, eu-gb` and causes all resources to fail evaluation.

### P2: CBR allowed public IPs (single entry, comma-separated)
{: #cspm-parameter-family-p2}

Controls
:   *Check whether `<service>` can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled*. These controls are available in the Controls Library and are included in the {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy for 32 services under requirements AC-4, SC-7(4)(a), and CP-9(d).

UI label
:   *This list has one element: the list of allowed Ips for CBR split by commas*. Input type: list (chips), using exactly one chip.

What it checks
:   For each evaluated resource:

    1. Context-based restrictions (CBR) must restrict service endpoints.
    1. If CBR rules allow public IP addresses, each allowed IP address must appear in your list.

    If CBR rules allow no public IP addresses, the control passes regardless of parameter values.

Although the phrase `with MFA enabled` appears in control names, the MFA setting is not evaluated. {{site.data.keyword.cloud_notm}} reports endpoints as unrestricted when public endpoints are accessible without MFA.
{: note}

What to enter
:   All public IP addresses, IP ranges, and CIDR blocks permitted in your CBR network zones in a single chip, separated by commas. Spaces after commas are permitted.

Where to find values in {{site.data.keyword.cloud_notm}}
:   Go to **Manage** > **Context-based restrictions** > **Network zones**, or run `ibmcloud cbr zones`. To verify which zones apply to a service, check **Manage** > **Context-based restrictions** > **Rules** or run `ibmcloud cbr rules`.

Format
:   `ip_or_cidr,ip_or_cidr,...` in one chip. Enter each value exactly as defined in the network zone.

Examples
:   * Valid single chip: `203.0.113.10,198.51.100.0/24`
    * Valid single chip with spaces: `203.0.113.10, 203.0.113.11, 198.51.100.0/24`
    * Incorrect: Two separate chips `203.0.113.10` and `198.51.100.0/24`. Only the first chip is evaluated; resources matching the second chip fail.
    * Incorrect: `198.51.100.0/16` entered to cover `198.51.100.0/24`. The comparison performs an exact string match.

Additional considerations
:   * With an empty parameter, the control passes only for resources whose CBR rules allow no public IP addresses.
    * {{site.data.keyword.bpshort}} is evaluated on the {{site.data.keyword.bpshort}} workspace resource.

### P3: CBR enforcement and allowed public IPs (two entries)
{: #cspm-parameter-family-p3}

Controls
:   *Check whether `<service>` can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled*, for Cloud Object Storage, Kubernetes Service, Event Notifications, Hyper Protect Crypto Services, Event Streams, Secrets Manager, and Key Protect. These seven controls are available in the Controls Library and are included in the {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy under requirements AC-4 and SC-7(4)(a).

UI label
:   *This list has two elements. First: CBR, second: the list of allowed Ips for CBR split by commas*. Input type: list (chips), using one or two chips.

What it checks
:   The resource must be protected by an enforced CBR rule (compared against the first chip). In addition, one of the following conditions must be met:

    * The CBR rule restricts endpoints and allows no public IP addresses.
    * The CBR rule restricts endpoints and every allowed public IP address is included in the second chip.
    * The service enforces private-only access natively: {{site.data.keyword.containershort_notm}} with the public service endpoint disabled, {{site.data.keyword.en_short}} with private endpoints, {{site.data.keyword.hscrypto}} with private-only network access, or {{site.data.keyword.messagehub}} with private networking enabled. For {{site.data.keyword.cos_full_notm}}, the second chip is also compared against bucket firewall IP addresses, and buckets whose CBR rules permit VPCs or services pass.

    With an empty parameter, the control always fails.

What to enter
:   * Chip 1: The literal text `cbr` (lowercase).
    * Chip 2 (only if CBR rules allow public IP addresses): All permitted public IP addresses and CIDR blocks in one chip, separated by commas, entered exactly as defined in the network zone.

Where to find values in {{site.data.keyword.cloud_notm}}
:   Go to **Manage** > **Context-based restrictions**.

Examples
:   * No public IP addresses permitted: One chip `cbr`
    * Public IP addresses permitted: Chip 1 `cbr`, Chip 2 `203.0.113.10,198.51.100.0/24`
    * Incorrect: `cbr,203.0.113.10` in a single chip. The first chip must contain only `cbr`.
    * Incorrect: Chip 1 `cbr`, Chip 2 `203.0.113.10`, Chip 3 `198.51.100.0/24`. Any chips after the second chip are ignored.

For the {{site.data.keyword.keymanagementserviceshort}} control in this family, specify only Chip 1 (`cbr`). {{site.data.keyword.keymanagementserviceshort}} instances with an enforced CBR rule that restricts endpoints then pass evaluation.
{: note}

### P4: CBR allowlist: wildcards and wide flows
{: #cspm-parameter-family-p4}

Controls
:   *Check whether there are no wild cards and wide flows in the private and public endpoints allow list for `<service>` (Context-based restrictions or service)*, for 38 services. These controls are available in the Controls Library and are included in the {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy under requirements AC-4, SC-7(5), SC-7(4)(h), and CP-9(d).

UI label
:   *Maximum length of netmask bit*. Input type: number.

What it checks
:   Only resources with CBR enabled are evaluated. For those resources:

    1. The private and public allowlists must not contain wildcards.
    1. The netmask prefix length reported for the allowlist (`max_netmask_bits_length`) must be greater than or equal to the specified number.

What to enter
:   The minimum CIDR prefix length that you accept. The prefix length is the number following the slash: `/24` corresponds to `24`, and a single IP address corresponds to `32`.

Where to find values in {{site.data.keyword.cloud_notm}}
:   Check IP addresses and subnets in **Manage** > **Context-based restrictions** > **Network zones**.

Examples
:   * `24`: Rejects entries wider than a `/24` subnet.
    * `32`: Permits only single IP addresses (`/32`).
    * `16`: Permits subnet ranges up to `/16`.

The default value is `0`, which applies only the wildcard validation check. Entering `0` resets the control to the default value.
{: note}

### P5: IP allowlists compared as exact text
{: #cspm-parameter-family-p5}

For the following five controls, each IP address or CIDR block configured in {{site.data.keyword.cloud_notm}} must appear in the parameter written exactly the same way. CIDR ranges do not cover narrower ranges or individual IP addresses. Use one chip per IP address or CIDR block.

| Control | UI label | What it checks | Default effect | Location in {{site.data.keyword.cloud_notm}} console |
| --- | --- | --- | --- | --- |
| Check whether Cloud Object Storage network access is restricted to a specific IP range | *Ip Allowlist For Cos* | Every IP in the bucket firewall (or bucket CBR allowlist) is in your list. A bucket with no firewall IPs and no CBR IPs fails. A bucket whose CBR rule allows VPCs or services passes. | Default `[""]` almost always fails. | {{site.data.keyword.cos_full_notm}} > bucket > Permissions > Firewall (legacy); CBR rules for the bucket |
| Check whether Public Access to IBM Cloud File Storage is blocked | *Ip Allowlist For Cbr* | CBR restricts the endpoints, and every allowed IP is in your list (or no IPs are allowed). | Empty value always fails, even for compliant shares. Enter at least one approved IP. | Manage > Context-based restrictions |
| Check whether Key Protect Single Tenant can be accessed only through a private endpoint (CBR or service) and public allowed IPs with MFA enabled | *Ip Allowlist For Cbr* | CBR restricts the endpoints, and every allowed IP is in your list (or no IP is allowed). | Empty value always passes. | Manage > Context-based restrictions |
| Check whether VPC security groups have inbound ports that are open only to permitted IP addresses | *Ip/Cidr List Allowed For Vpc Inbound* | The source CIDR of every inbound rule is in your list. | Empty value always passes. | VPC Infrastructure > Security groups > rules (Source) |
| Check whether VPC security groups have outbound ports that are open only to permitted IP addresses | *Ip/Cidr List Allowed For Vpc Outbound* | The destination CIDR of every outbound rule is in your list. | Empty value always passes. | VPC Infrastructure > Security groups > rules (Destination) |
{: caption="Parameters for IP allowlists evaluated as exact text" caption-side="bottom"}

Examples
:   * {{site.data.keyword.cos_full_notm}} firewall: `10.20.0.0/24`, `203.0.113.10`
    * Security group inbound: `10.20.0.0/16`, `192.0.2.0/24`, `0.0.0.0/0` (only if any source is permitted)
    * Incorrect: Entering `10.0.0.0/8` to cover `10.20.0.0/16`. Comparisons use exact text matching.

When configuring security group parameters, rules whose source or destination is another security group or a single IP address (rather than a CIDR format) fail evaluation because only the CIDR field is evaluated. Specify individual IP addresses in CIDR format in {{site.data.keyword.cloud_notm}} (`203.0.113.10/32`) and list them the same way in the parameter.
{: note}

### P6: IP allowlists compared as CIDR ranges
{: #cspm-parameter-family-p6}

The following three controls evaluate whether an IP address falls within a defined CIDR range. Enter one chip per entry; do not combine multiple CIDRs into a single chip unless specified. These controls are available in the Controls Library and are included in the {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy.

#### Check whether public Load Balancers for VPC only allow inbound traffic from allowed IP ranges
{: #p6-public-load-balancers}

Requirements
:   AC-4, SC-7(10)(a), SC-7(4)(a), SC-7(5), CM-7(a)

UI label
:   *Allowed inbound sources for public load balancers: `<ip_or_cidr>`*

What it checks
:   Every inbound rule of each security group attached to a public {{site.data.keyword.alb_full}} or {{site.data.keyword.nlb_full}} must have its source within one of your configured entries. Rules that specify another security group as the source pass. A public load balancer with no attached security group fails unless `0.0.0.0/0` is listed.

Default
:   The IPv4 and IPv6 ranges of {{site.data.keyword.cis_full_notm}} proxies, published in the [CIS public IP list](https://api.cis.cloud.ibm.com/v1/ips). This default is designed for load balancers reached exclusively through CIS.

What to enter
:   One IP address or CIDR block per chip (IPv4 or IPv6). Retain CIS ranges if {{site.data.keyword.cis_short_notm}} is used, and add your organization-specific entries.

Examples
:   `192.0.2.0/24`, `198.51.100.10`, `2001:db8::/32`

Incorrect
:   `192.0.2.0/24, 198.51.100.10` in a single chip.

Where to find values in {{site.data.keyword.cloud_notm}}
:   Go to **VPC Infrastructure** > **Load balancers** > *load balancer* > **Security groups** > **Rules**.

#### Check whether VPC network ACLs allow ingress only from allowed IPs per attached subnet
{: #p6-vpc-acls-ingress}

Requirements
:   AC-4, SC-7(10)(a), SC-7(4)(a), SC-7(5), CM-7(a)

UI label
:   *Allowed ingress per subnet: `<subnet_cidr>[,...]=<allowed_cidr>[,...]`*

What it checks
:   For each subnet attached to the ACL, every inbound allow rule must have its source within the permitted sources for that subnet. Deny rules are ignored.

Format
:   One chip per network zone using the format `<subnet CIDRs, comma-separated>=<allowed source IPs/CIDRs, comma-separated>`. A subnet key also covers subnets within that range. Multiple chips for the same subnet are combined.

Examples
:   * `10.10.0.0/24,10.10.1.0/24=192.0.2.0/24,198.51.100.10`
    * `10.10.0.0/16=10.0.0.0/8` (all subnets in `10.10.0.0/16` accept traffic from `10.0.0.0/8`)

Default effect
:   With an empty parameter, all inbound allow rules fail evaluation.

Where to find values in {{site.data.keyword.cloud_notm}}
:   Go to **VPC Infrastructure** > **Access control lists** (rules) and **VPC Infrastructure** > **Subnets** (IP ranges).

#### Check whether VPC network ACLs allow egress only to allowed IPs and ports per attached subnet
{: #p6-vpc-acls-egress}

Requirements
:   AC-4, SC-7(10)(a), SC-7(4)(a), SC-7(5), CM-7(a)

UI label
:   *Allowed egress per subnet: `<subnet_cidr>[,...]=<allowed_cidr>[,...]=<port_min>-<port_max>`*

What it checks
:   For each attached subnet, every outbound allow rule must target an allowed destination within the specified port range. ICMP rules ignore ports. Protocols without port numbers (such as `all`) require the full port range `1-65535`.

Format
:   One chip per zone and port range using the format `<subnet CIDRs>=<allowed destinations>=<port_min>-<port_max>`. A single port can be entered as `443`. To allow multiple port ranges, create a separate chip for each range.

Examples
:   * `10.10.0.0/24=203.0.113.0/24=443`
    * `10.10.0.0/24=203.0.113.0/24=8080-8090`
    * `10.10.0.0/16=161.26.0.0/16=1-65535` ({{site.data.keyword.cloud_notm}} service endpoints, all ports)

Default effect
:   With an empty parameter, all outbound allow rules fail evaluation.

### P7: Exclusion lists by resource name
{: #cspm-parameter-family-p7}

The control is evaluated normally, but resources whose names are included in the exclusion list pass evaluation. Enter one resource name per chip, matching the name in {{site.data.keyword.cloud_notm}} exactly (case-sensitive). These controls are available in the Controls Library and are included in the {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy.

| Control | UI label | Value to enter | Example |
| --- | --- | --- | --- |
| Check whether Virtual Servers for VPC instance has all interfaces with IP-spoofing disabled | *Exclude Interfaces With Ip-Spoofing From Vpc* | Names of the {{site.data.keyword.vsi_is_short}} instances that must keep IP spoofing enabled (for example, third-party network appliances) | `myorg-net-appliance-01` |
| Check whether Application Load Balancer for VPC has public access disabled | *Exclude Load Balancers* | Names of the {{site.data.keyword.alb_full}} instances that are permitted to be public | `myorg-public-alb-web` |
| Check whether Virtual Private Cloud (VPC) has no subnet with public gateway attached | *Exclude Subnets* | Names of the subnets that are permitted to have a public gateway | `myorg-egress-subnet-z1` |
| Check whether a security group other than the default for Virtual Private Cloud is attached to all endpoints | *Exclude The Security Groups* | Names of the security groups to exclude | `myorg-vpc-default-sg` |
| No containers with docker.sock mounted *(agent control)* | *Excluded container names or IDs* | A container ID (exact match) or the start of a container name | `node-exporter`, `3f4e2a1b9c7d` |
{: caption="Parameters for exclusion lists by resource name" caption-side="bottom"}

Where to find values in {{site.data.keyword.cloud_notm}}
:   Check the **Name** column in **VPC Infrastructure** > **Virtual server instances**, **Load balancers**, **Subnets**, or **Security groups**, or run `ibmcloud is instances`, `ibmcloud is load-balancers`, `ibmcloud is subnets`, or `ibmcloud is security-groups`.

### P8: Lists of allowed values
{: #cspm-parameter-family-p8}

The following controls are available in the Controls Library and are included in the {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy.

#### VPN and cryptography
{: #p8-vpn-crypto}

The following table lists the parameters for VPN and cryptography controls.

| Control | UI label | Value to enter (one per chip) | Default | Location in {{site.data.keyword.cloud_notm}} console |
| --- | --- | --- | --- | --- |
| Check whether VPN Authentication methods are set as appropriate | *Allowed VPN Authentication Modes* | `certificate` or `username` (user ID and passcode). The control fails if a client-to-site server uses any method that is not listed. | `certificate` | VPC Infrastructure > VPNs > Client-to-site servers > server > Client authentication |
| Check whether IBM VPN For VPC Connection IKE Policy encryption is set as appropriate | *Allowed Encryption Method* | IKE encryption algorithms, {{site.data.keyword.IBM_notm}} API names: `aes128`, `aes192`, `aes256` | `aes128`, `aes192`, `aes256` | VPC Infrastructure > VPNs > IKE policies |
| Check whether IBM VPN For VPC Connection IPSEC Policy encryption is set as appropriate | *Allowed Encryption Method* | IPsec encryption algorithms: `aes128`, `aes192`, `aes256`, `aes128gcm16`, `aes192gcm16`, `aes256gcm16` | All six algorithms | VPC Infrastructure > VPNs > IPsec policies |
| Check whether IBM Client VPN cipher is set as appropriate | *Allowed SSL/TLS Ciphers for VPN server* | The cipher exactly as written after the word `cipher` in the client configuration of the VPN server (case-insensitive) | List of TLS cipher suites (see notes) | VPC Infrastructure > VPNs > Client-to-site servers > server > **Download client profile**, check the `cipher` entry |
{: caption="Parameters for VPN and cryptography controls" caption-side="bottom"}

Site-to-site connections that use auto-negotiation (no IKE or IPsec policy attached) are not evaluated by the two encryption controls.

Client VPN cipher
:   The default list contains TLS cipher suite names (`ECDHE-...`). If the client profile contains a data-channel cipher such as `cipher AES-256-GCM`, add that exact value (such as `AES-256-GCM` or `AES-128-GCM`), or the control fails. Remove deprecated ciphers such as `EDH-RSA-DES-CBC3-SHA` (3DES) from the list.

#### Network placement and images
{: #p8-network-images}

The following table lists the parameters for network placement and image controls.

| Control | UI label | Value to enter (one per chip) | Default effect | Location in {{site.data.keyword.cloud_notm}} console |
| --- | --- | --- | --- | --- |
| Check whether Virtual Private Cloud is configured with public gateways that are provisionable only within permitted zones | *Ibm Cloud Public Gateway Permitted Zones* | Zone names where public gateways are permitted: `eu-de-1`, `eu-de-2`, `eu-de-3` | Empty value: every public gateway fails | `ibmcloud is zones <region>`; VPC Infrastructure > Public gateways (Zone) |
| Check whether virtual servers for VPC is provisioned from customer-defined list of images | *Vpc Provisioned From Customer-Defined Images* | Image names (not IDs), for example `ibm-redhat-9-4-minimal-amd64-5` or your custom image `myorg-golden-rhel9-2026-10` | Empty value: every virtual server fails | `ibmcloud is images` (NAME column); VPC Infrastructure > Images |
| Check that Hyper Protect Crypto Services has failover units in at least 2 different regions | *Hyper Protect Crypto Services Regions* | Regions accepted for failover crypto units, for example `eu-de`, `eu-gb` | Empty value: always fails | {{site.data.keyword.hscrypto}} instance > Overview (failover crypto units) |
{: caption="Parameters for network placement and image controls" caption-side="bottom"}

{{site.data.keyword.IBM_notm}} stock image names include a revision number (`...-amd64-5`). When new image revisions are published, update the parameter with the new revision name to prevent evaluations from failing.

{{site.data.keyword.hscrypto}} failover
:   The instance must have failover crypto units in a region different from the primary instance region and included in your configured list. Instances without failover crypto units cannot pass. If your deployment uses a single region by design, create a risk acceptance for this control.

#### Services, logging, and tooling
{: #p8-services-logging-tooling}

The following table lists the parameters for services, logging, and tooling controls.

| Control | UI label | Value to enter (one per chip) | Default effect | Location in {{site.data.keyword.cloud_notm}} console |
| --- | --- | --- | --- | --- |
| Check whether Event Notifications is configured for each of the supported Services | *Services Configured For Event Notifications* | {{site.data.keyword.en_short}} source types, for example `secrets-manager`, `sysdig-monitor`, `compliance`, `cloud-object-storage` | Empty value: always fails | {{site.data.keyword.en_short}} instance > Sources |
| Check that Cloud Logs is configured to collect global events generated by IBM Cloud services from the appropriate locations | *Regions Where Cloud Logs should be retrieving Logs* | Regions, for example `eu-de`, `eu-gb` | Empty value: always passes | {{site.data.keyword.logs_full_notm}} instance > Streams / Logs Routing |
| Check whether the desired IBM services are Financial Services Validated | *Services that must have Financial Services Validation enabled* | {{site.data.keyword.IBM_notm}} service names picked from the suggestions, for example `kms`, `hs-crypto`, `cloud-object-storage`, `containers-kubernetes`, `logs` | Empty value: always passes | {{site.data.keyword.cloud_notm}} catalog, *Financial Services Validated* filter |
| Checks whether Toolchain is configured only with the allowed integration tools | *Allowed Tool Integration Services For Toolchains* | Toolchain tool type IDs, for example `hostedgit`, `github`, `pipeline`, `secretsmanager`, `keyprotect`, `slack` | Empty value: every toolchain with at least one tool fails | {{site.data.keyword.contdelivery_short}} > Toolchains > toolchain (tool integrations); Toolchain API `GET /toolchains/{id}/tools` (`tool_type_id`) |
{: caption="Parameters for services, logging, and tooling controls" caption-side="bottom"}

{{site.data.keyword.en_short}}
:   The control currently passes if at least one of the listed source types is configured on the instance.

Toolchains
:   The control currently passes if at least one tool configured in the toolchain appears in the list.

Financial Services Validated suggestions
:   `billing`, `schematics`, `transit`, `atracker`, `cloud-object-storage`, `hs-crypto`, `codeengine`, `sysdig-secure`, `toolchain`, `cloudantnosqldb`, `databases-for-mongodb`, `databases-for-redis`, `iam-identity`, `containers-kubernetes`, `resource-controller`, `container-registry`, `apprapp`, `globalcatalog-collection`, `appid`, `internet-svcs`, `project`, `power-iaas`, `messagehub`, `kms`, `sysdig-monitor`, `continuous-delivery`, `pm-20`, `conversation`, `logs`, `data-science-experience`, `aiopenscale`, `metrics-router`, `iam-groups`, `directlink`, `watsonx-orchestrate`, `databases-for-elasticsearch`, `dns-svcs`, `messages-for-rabbitmq`, `instructlab`, `event-notifications`.

#### Account and endpoint settings
{: #p8-account-endpoints}

The following table lists the parameters for account and endpoint settings controls.

| Control | UI label | Value to enter | Default | Notes |
| --- | --- | --- | --- | --- |
| Check whether an Account has Direct Link enabled following your company policy | *Organizational Policy to see if directlink should be disabled/enabled (only the first parameter will be considered)* | Exactly one chip: `disabled` or `enabled` | `disabled` | `disabled`: fails if the account has any {{site.data.keyword.dl_short}}. `enabled`: passes if {{site.data.keyword.dl_short}} is present. |
| Check whether Key Protect can be accessed only through a private endpoint (Context-based restrictions or service) | *Check For Cbr Enforcement* | `cbr` or `service` (one per chip) | Empty value: always fails | `cbr`: passes when an enforced CBR rule restricts {{site.data.keyword.keymanagementserviceshort}} to private endpoints. `service`: passes when the instance enforces private endpoints at the service level. Recommended: both `cbr` and `service` chips. |
{: caption="Parameters for account and endpoint settings" caption-side="bottom"}

#### Agent controls (Kubernetes workloads)
{: #p8-agent-controls}

The following table lists the parameters for Kubernetes workload agent controls.

| Control | UI label | Value to enter (one per chip) | Default effect |
| --- | --- | --- | --- |
| Approved Registries | *List of Approved Registries* | Registry host, optionally with a namespace path, without `https://`: `icr.io`, `de.icr.io`, `de.icr.io/myorg-prod`. An image passes if it starts with `<value>/`. | Empty value: every workload fails. |
| Container with Forbidden Capabilities | *List of Forbidden Capabilities* | Select from suggestions (free text is not accepted). The list contains capabilities containers must not have. Remove capabilities that you accept. | Default includes all 37 capabilities: a container passes only if it drops all capabilities. |
{: caption="Parameters for Kubernetes workload agent controls" caption-side="bottom"}

For *Approved Registries*, enter one registry per chip and omit `https://`.
{: tip}

### P9: IAM entity lists
{: #cspm-parameter-family-p9}

These controls are available in the Controls Library and are included in the {{site.data.keyword.framework-fs_notm}} 2.0 v2.0 policy under requirements AC-6(1)(a) and AC-6(2). Enter one entity name per chip: a user, access group, or service ID, matching the name in {{site.data.keyword.cloud_notm}} exactly. You can copy the name from the IAM resource in {{site.data.keyword.sysdigsecure_short}} **Inventory**.

A subject is evaluated as having full permission when an access policy grants two or more in-scope roles (such as Administrator, Editor, Operator, Manager, Writer, or Key Manager), or a custom role that can create, delete, or modify keys.

The following table lists the parameters for IAM entity list controls.

| Control | UI label | Meaning of the list | Default effect |
| --- | --- | --- | --- |
| Check whether Access Policy grants full Key Protect:* permissions only to desired users/groups/serviceIds | *Name of Allowed Entities (Users, Access Groups or ServiceIds) that have full KeyProtect Permissions* | Allowlist. Any subject with full permission that is not in the list fails. Include the account owner. | Empty value: always passes. |
| Check whether Access Policy does not grant full Key Protect:* permissions to non-dedicated users/groups/serviceIds | *Name of Forbidden Entities…* | Denylist. Any subject in the list that holds full permission fails. | Empty value: always passes. |
| Check whether Access Policy grants full Hyper Protect Crypto Services permissions only to desired users/groups/serviceIds | None | Allowlist, similar to the {{site.data.keyword.keymanagementserviceshort}} control. Only policies that target {{site.data.keyword.hscrypto}} are evaluated. | Always passes. |
{: caption="Parameters for IAM entity list controls" caption-side="bottom"}

The {{site.data.keyword.keymanagementserviceshort}} controls evaluate policies based on granted platform roles (such as Administrator and Editor) regardless of whether the policy specifically targets {{site.data.keyword.keymanagementserviceshort}}. Additionally, the {{site.data.keyword.hscrypto}} control currently does not provide a parameter field in the console and always passes evaluation.
{: note}

Examples
:   `myorg-kms-admins` (access group), `ServiceId-kms-rotator` (service ID), `Public Access` (built-in access group, denylist).

## Appendix A: all parameterized controls
{: #appendix-parameterized-controls}

The following table lists all parameterized controls and default values. List types are chips, and you must enter values individually unless otherwise specified. Number types include an input box where you can provide a numerical value.

The default effect indicates the posture behavior when the default value is set. Always fails and Always passes indicate that the result does not reflect your actual environment security posture until the values are customized.

| No. | Control name | Family | FS 2.0 v2.0 requirements | Type | Default | Default effect |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Check whether IBM Activity Tracker Event Routing Route is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 2 | Check whether IBM Activity Tracker Event Routing Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 3 | Check whether IBM Activity Tracker Event Routing Target is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 4 | Check whether IBM App Id Cloud Directory Advanced Password Policy is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 5 | Check whether IBM App Id Cloud Directory Configuration is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 6 | Check whether IBM App Id Cloud Directory Custom Email Dispatcher Configuration is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 7 | Check whether IBM App Id Redirect Uri is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 8 | Check whether IBM Billing Account Trait is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 9 | Check whether IBM Catalog Management Account Settings is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 10 | Check whether IBM Cloud Activity Tracker Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 11 | Check whether IBM Cloud File Storage Instance is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 12 | Check whether IBM Cloud Logs Alert is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 13 | Check whether IBM Cloud Logs Data Access Rule is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 14 | Check whether IBM Cloud Logs Enrichment is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 15 | Check whether IBM Cloud Logs Events To Metrics is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 16 | Check whether IBM Cloud Logs Instance is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 17 | Check whether IBM Cloud Logs Outgoing Webhook is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 18 | Check whether IBM Cloud Logs Policy is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 19 | Check whether IBM Cloud Logs Router Tenant is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 20 | Check whether IBM Cloud Logs Rule Group is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 21 | Check whether IBM Cloud Logs Stream is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 22 | Check whether IBM Cloud Logs View is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 23 | Check whether IBM Cloud Object Storage Bucket is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 24 | Check whether IBM Cloud Shell Account Settings is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 25 | Check whether IBM Code Engine Project is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 26 | Check whether IBM Container Registry Image is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 27 | Check whether IBM Container Registry Namespace is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 28 | Check whether IBM Container Registry Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 29 | Check whether IBM Direct Link Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 30 | Check whether IBM Event Notifications Source is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 31 | Check whether IBM Hyper Protect Crypto Services Key is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 32 | Check whether IBM IAM Access Groups Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 33 | Check whether IBM IAM Access Management Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 34 | Check whether IBM IAM Access Policy is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 35 | Check whether IBM IAM Identity Service APIKEY is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 36 | Check whether IBM IAM Identity Service Account Settings is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 37 | Check whether IBM IAM Identity Service CBR Resource is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 38 | Check whether IBM IAM Identity Service Id is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 39 | Check whether IBM IAM Role is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 40 | Check whether IBM IAM Identity Service Global Catalog Resource is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 41 | Check whether IBM IAM Identity Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 42 | Check whether IBM Internet Services Zone is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 43 | Check whether IBM Key Protect Key is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 44 | Check whether IBM Kubernetes Service Openshift Cluster is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 45 | Check whether IBM Kubernetes Service Secret is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 46 | Check whether IBM Kubernetes Service Worker is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 47 | Check whether IBM Load Balancer Listener For VPC Instance is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 48 | Check whether IBM Load Balancer Listener Policy For VPC Instance is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 49 | Check whether IBM Load Balancer Pool For VPC Instance is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 50 | Check whether IBM Log Analysis Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 51 | Check whether IBM Network ACL Rule is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 52 | Check whether IBM PowerVS Instance is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 53 | Check whether IBM PowerVS Network Address Group is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 54 | Check whether IBM PowerVS Network Instance is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 55 | Check whether IBM PowerVS Network Interface is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 56 | Check whether IBM PowerVS Network Security Group is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 57 | Check whether IBM PowerVS Network is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 58 | Check whether IBM PowerVS Volume is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 59 | Check whether IBM PowerVS Workspace is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 60 | Check whether IBM Secrets Manager Secret Group is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 61 | Check whether IBM Secrets Manager Secret is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 62 | Check whether IBM Security Group For VPC Rule is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 63 | Check whether IBM Transit Gateway Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 64 | Check whether IBM User Management Owner is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 65 | Check whether IBM User Management Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 66 | Check whether IBM User Management User is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 67 | Check whether IBM VPN For VPC Connection is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 68 | Check whether IBM VPN For VPC Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 69 | Check whether IBM Virtual Private Cloud Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 70 | Check whether IBM Watson Machine Learning Project is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 71 | Check whether IBM Watson Machine Learning Service is provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 72 | Check whether IBM resources are provisioned in allowed region | P1 | SC-7(a), SC-7(5), CM-7(a) | List | `[]` | Always passes |
| 73 | Check whether App Configuration can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 74 | Check whether Auto scale for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 75 | Check whether Backup for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a), CP-9(d) | List | `[]` | Meaningful |
| 76 | Check whether Bare Metal Servers for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 77 | Check whether Block Storage Snapshots for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 78 | Check whether Block Storage for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 79 | Check whether Client VPN for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 80 | Check whether Code Engine can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 81 | Check whether Container Registry can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 82 | Check whether DNS Services can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 83 | Check whether Dedicated Host for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 84 | Check whether Direct Link can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 85 | Check whether Flow Logs for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 86 | Check whether IAM access groups can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 87 | Check whether IAM access management can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 88 | Check whether Load Balancer for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 89 | Check whether Schematics can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 90 | Check whether Security and Compliance Center can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 91 | Check whether Transit Gateway can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 92 | Check whether User Management can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 93 | Check whether VPC SSH keys can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 94 | Check whether VPC floating IPs can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 95 | Check whether VPC images can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 96 | Check whether VPC network access control lists can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 97 | Check whether VPC placement groups can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 98 | Check whether VPC public gateways can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 99 | Check whether VPC security groups can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 100 | Check whether VPC subnets can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 101 | Check whether VPN for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 102 | Check whether Virtual Private Cloud can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 103 | Check whether Virtual Private Endpoints for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 104 | Check whether Virtual Servers for VPC can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P2 | AC-4, SC-7(4)(a) | List | `[]` | Meaningful |
| 105 | Check whether Cloud Object Storage can be accessed only through a private endpoint or direct endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P3 | AC-4, SC-7(4)(a) | List | `[]` | Always fails |
| 106 | Check whether Event Notifications can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P3 | AC-4, SC-7(4)(a) | List | `[]` | Always fails |
| 107 | Check whether Event Streams can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P3 | AC-4, SC-7(4)(a) | List | `[]` | Always fails |
| 108 | Check whether Hyper Protect Crypto Services can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P3 | AC-4, SC-7(4)(a) | List | `[]` | Always fails |
| 109 | Check whether Key Protect can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P3 | SC-7(4)(a) | List | `[]` | Always fails |
| 110 | Check whether Kubernetes Service can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P3 | AC-4, SC-7(4)(a) | List | `[]` | Always fails |
| 111 | Check whether Secrets Manager can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P3 | AC-4, SC-7(4)(a) | List | `[]` | Always fails |
| 112 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for App Configuration (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 113 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Auto Scale for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 114 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Backup for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5), CP-9(d) | Number | 0 | Meaningful |
| 115 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Bare Metal Servers for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 116 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Block Storage Snapshots for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 117 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Block Storage for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 118 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Client VPN for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 119 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Cloud Object Storage (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 120 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Code Engine (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 121 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Container Registry (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 122 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for DNS Services (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 123 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Dedicated Host for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 124 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Direct Link (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 125 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Event Notifications (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 126 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Event Streams (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 127 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Flow Logs for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 128 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Hyper Protect Crypto Services (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 129 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for IAM access groups (Context-based restrictions or service) | P4 | AC-4, SC-7(4)(h), SC-7(5) | Number | 0 | Meaningful |
| 130 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for IAM access management (Context-based restrictions or service) | P4 | AC-4, SC-7(4)(h), SC-7(5) | Number | 0 | Meaningful |
| 131 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Kubernetes Service (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 132 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Load Balancer for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 133 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Schematics (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 134 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Secrets Manager (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 135 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Security and Compliance Center (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 136 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Transit Gateway (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 137 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for User Management (Context-based restrictions or service) | P4 | AC-4, SC-7(4)(h), SC-7(5) | Number | 0 | Meaningful |
| 138 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPC SSH key (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 139 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPC floating IPs (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 140 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPC images (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 141 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPC network access control lists (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 142 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPC placement groups (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 143 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPC public gateways (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 144 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPC security groups (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 145 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPC subnets (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 146 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for VPN for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 147 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Virtual Private Cloud (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 148 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Virtual Private Endpoints for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 149 | Check whether there are no wild cards and wide flows in the private and public endpoints allow list for Virtual Servers for VPC (Context-based restrictions or service) | P4 | AC-4, SC-7(5) | Number | 0 | Meaningful |
| 150 | Check whether Cloud Object Storage network access is restricted to a specific IP range | P5 | AC-4, SC-7(b) | List | `[""]` | Always fails |
| 151 | Check whether Key Protect Single Tenant can be accessed only through a private endpoint (Context-based restrictions or service) and public allowed IPs with MFA enabled | P5 | SC-7(4)(a) | List | `[]` | Always passes |
| 152 | Check whether Public Access to IBM Cloud File Storage is blocked | P5 | AC-4, AC-14(a), SC-7(b) | List | `[]` | Always fails |
| 153 | Check whether Virtual Private Cloud (VPC) security groups have inbound ports that are open only to permitted IP addresses | P5 | AC-4, SC-7(a), CM-7(a) | List | `[]` | Always passes |
| 154 | Check whether Virtual Private Cloud (VPC) security groups have outbound ports that are open only to permitted IP addresses | P5 | AC-4, SC-7(10)(a), CM-7(a) | List | `[]` | Always passes |
| 155 | Check whether VPC network ACLs allow egress only to allowed IPs and ports per attached subnet | P6 | AC-4, SC-7(10)(a), SC-7(4)(a), SC-7(5), CM-7(a) | List | `[]` | Always fails |
| 156 | Check whether VPC network ACLs allow ingress only from allowed IPs per attached subnet | P6 | AC-4, SC-7(10)(a), SC-7(4)(a), SC-7(5), CM-7(a) | List | `[]` | Always fails |
| 157 | Check whether public Load Balancers for VPC only allow inbound traffic from allowed IP ranges | P6 | AC-4, SC-7(10)(a), SC-7(4)(a), SC-7(5), CM-7(a) | List | 22 values (CIS ranges) | Meaningful |
| 158 | Check whether Application Load Balancer for VPC has public access disabled | P7 | AC-4, SC-7(4)(a), CM-7(a) | List | `[]` | Meaningful |
| 159 | Check whether Virtual Private Cloud (VPC) has no subnet with public gateway attached | P7 | AC-4, SC-7(c) | List | `[]` | Meaningful |
| 160 | Check whether Virtual Servers for VPC instance has all interfaces with IP-spoofing disabled | P7 | AC-4, SC-7(a), CM-7(a) | List | `[]` | Meaningful |
| 161 | Check whether a security group other than the default for Virtual Private Cloud is attached to all endpoints | P7 | AC-4, SC-7(a) | List | `[""]` | Meaningful |
| 162 | No containers with docker.sock mounted | P7 | CM-6(b) | List | `[]` | Meaningful |
| 163 | Approved Registries | P8 | CM-6(a) | List | `[]` | Always fails |
| 164 | Check that Cloud Logs is configured to collect global events generated by IBM Cloud services from the appropriate locations | P8 | AC-16(e) | List | `[]` | Always passes |
| 165 | Check that Hyper Protect Crypto Services has failover units in at least 2 different regions | P8 | CP-6(1), CP-7(1) | List | `[]` | Always fails |
| 166 | Check whether Event Notifications is configured for each of the supported Services | P8 | SI-4(g) | List | `[]` | Always fails |
| 167 | Check whether IBM Client VPN cipher is set as appropriate | P8 | SC-13(b) | List | 18 values (TLS suites) | Meaningful |
| 168 | Check whether IBM VPN For VPC Connection IKE Policy encryption is set as appropriate | P8 | SC-13(b) | List | `["aes128", "aes192", "aes256"]` | Meaningful |
| 169 | Check whether IBM VPN For VPC Connection IPSEC Policy encryption is set as appropriate | P8 | SC-13(b) | List | 6 values (see guide) | Meaningful |
| 170 | Check whether Key Protect can be accessed only through a private endpoint (Context-based restrictions or service) | P8 | SC-7(4)(a) | List | `[]` | Always fails |
| 171 | Check whether VPN Authentication methods are set as appropriate | P8 | AC-4(21), AC-17(b), IA-3, SC-7(a), SA-10(a) | List | `["certificate"]` | Meaningful |
| 172 | Check whether Virtual Private Cloud is configured with public gateways that are provisionable only within permitted zones | P8 | AC-4, SC-7(c), CM-7(1)(b) | List | `[]` | Always fails |
| 173 | Check whether an Account has Direct Link enabled following your company policy | P8 | AC-4(21), SC-7(a) | List | `["disabled"]` | Meaningful |
| 174 | Check whether the desired IBM services are Financial Services Validated | P8 | AC-20(1)(a), SC-7(5), CM-6(b), CM-7(a) | List | `[]` | Always passes |
| 175 | Check whether virtual servers for VPC is provisioned from customer-defined list of images | P8 | CM-8(3)(a) | List | `[]` | Always fails |
| 176 | Checks whether Toolchain is configured only with the allowed integration tools | P8 | SA-15(a) | List | `[]` | Always fails |
| 177 | Container with Forbidden Capabilities | P8 | CM-7(a) | List | 37 values (all dropped) | Meaningful |
| 178 | Check whether Access Policy does not grant full Key Protect permissions to non-dedicated users/groups/serviceIds | P9 | AC-6(2) | List | `[]` | Always passes |
| 179 | Check whether Access Policy grants full Hyper Protect Crypto Services permissions only to desired users/groups/serviceIds | P9 | AC-6(1)(a) | List | `[]` | Always passes |
| 180 | Check whether Access Policy grants full Key Protect permissions only to desired users/groups/serviceIds | P9 | AC-6(1)(a) | List | `[]` | Always passes |
| 181 | Check whether App ID Cloud Directory lockout period is set to at least # minute(s) | P10 | AC-7(b) | Number | 0 | Always passes |
| 182 | Check whether App ID Cloud Directory minimum period between password changes policy is set to greater than 0 | P10 | IA-5(f) | Number | 0 | Meaningful |
| 183 | Check whether App ID access tokens are configured to expire within # minutes | P10 | SC-10 | Number | 0 | Always fails |
| 184 | Check whether Container Registry Vulnerability Advisor scans for critical or high vulnerabilities in the system at least every # day(s) | P10 | SI-2(a), SI-2(2), RA-5(a), CM-7(1)(a), SA-3(a), SA-3(d), SA-10(e), CA-2(2), CA-7(d) | Number | 7 | Meaningful |
| 185 | Check whether Hyper Protect Crypto Services encryption keys that are generated by the service are rotated automatically at least every # months | P10 | SC-12 | Number | 3 | Meaningful |
| 186 | Check whether Hyper Protect Crypto Services instance has at least # crypto units | P10 | SC-6, SC-12(2), CP-7(a) | Number | 1 | Meaningful |
| 187 | Check whether IBM Cloud Logs instance log retention is set to at least # days | P10 | AU-11, SI-12, CM-3(e) | Number | 7 | Meaningful |
| 188 | Check whether IBM Log Analysis instance log retention is set to at least # days | P10 | AU-11, SI-12 | Number | 0 | Always passes |
| 189 | Check whether Secrets Manager arbitrary secrets are rotated at least every # days | P10 | IA-5(f) | Number | 90 | Meaningful |
| 190 | Check whether Secrets Manager user credentials are rotated at least every # days | P10 | IA-5(f) | Number | 0 | Always fails |
| 191 | Check whether VPN for VPC authentication is configured with a strong pre-shared key with at least # characters | P10 | IA-5(c) | Number | 0 | Always passes |
| 192 | Check whether VPN for VPC has a Diffie-Hellman group set to at least group # | P10 | SC-13(b) | Number | 0 | Always passes |
| 193 | Check whether Virtual Servers for VPC instance has the minimum # interfaces | P10 | CM-7(a) | Number | 0 | Always passes |
| 194 | Check whether a Red Hat OpenShift cluster has at least # worker nodes across multiple zones | P10 | SC-6, CP-7(a) | Number | 0 | Always passes |
| 195 | Check whether an inactive user account has not been suspended | P10 | AC-2(f), AC-2(2), AC-2(3)(d) | Number | 90 | Meaningful |
| 196 | Check whether each Application Load Balancer for VPC is configured to use at least # zones | P10 | SC-6, CP-7(a) | Number | 0 | Always passes |
| 197 | Check whether each Virtual Private Cloud is configured to use at least # zones | P10 | SC-6, CP-7(a) | Number | 0 | Always passes |
| 198 | Check whether sign out due to inactivity is set to # seconds or less for IBM Cloud accounts | P10 | AC-11(a), SC-10 | Number | 900 | Meaningful |
| 199 | Check whether sign out for active sessions is set to # seconds or less for IBM Cloud accounts | P10 | SC-10 | Number | 28800 | Meaningful |
| 200 | Check whether the API key has an appropriate rotation period | P10 | IA-5(f) | Number | 90 | Meaningful |
| 201 | Check whether the API key has been used within an appropriate time period | P10 | AC-2(3)(d) | Number | 180 | Meaningful |
| 202 | Check whether there are at least # instances of Direct Link in an account | P10 | CP-8 | Number | 0 | Always passes |
| 203 | Check whether Key Protect Single Tenant can be accessed only through a private endpoint (Context-based restrictions or service) | P11 | SC-7(4)(a) | — | — | No effect |
| 204 | Check whether Security Groups for VPC contains no outbound rules in security groups that specify destination IP 8.8.8.8/32 to DNS port | P11 | AC-4, SC-7(10)(a), CM-7(b) | Number | 0 | No effect |
{: caption="Default parameter behavior for controls" caption-side="bottom"}
