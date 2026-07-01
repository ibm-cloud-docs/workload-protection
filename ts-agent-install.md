---

copyright:
  years:  2026
lastupdated: "2026-07-01"

keywords: agent installation, dragent service, agent troubleshooting, and kernel headers.

subcollection: workload-protection

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my agent fail to install or start after deployment?
{: #ts-agent-install}
{: troubleshoot}

The {{site.data.keyword.sysdigsecure_short}} agent does not start after installation, or the agent process is not visible in the host process list.
{: tsSymptoms}

The agent might fail to start for one of the following reasons:
{: tsCauses}

- The access key or collector endpoint is missing or incorrect in the agent configuration file (`/opt/draios/etc/dragent.yaml`).
- The collector endpoint is not reachable on port 6443. A firewall rule or security group is blocking outbound traffic.
- Kernel headers are not installed, which prevents the agent from loading its kernel module.
- The `dragent` service failed to start due to a configuration syntax error.
- The `universal_ebpf` driver is selected but the host kernel version is earlier than 5.8.

To resolve this issue, complete the following steps:
{: tsResolve}

1. Verify that the `dragent` service is running:

   ```sh
   systemctl status dragent
   ```
   {: pre}

2. Check the agent logs for errors:

   ```sh
   grep -i error /opt/draios/logs/draios.log
   ```
   {: pre}

3. Confirm that the agent process is running:

   ```sh
   ps -ef | grep sysdig
   ```
   {: pre}

4. Open `/opt/draios/etc/dragent.yaml` and verify that the `customerid`, `collector`, and `sysdig_api_endpoint` fields are set correctly. The collector endpoint must use port 6443 and SSL must be enabled (`ssl: true`).

5. Confirm that outbound TCP traffic to the collector endpoint on port 6443 is allowed. For a list of collector endpoints, see [Collector endpoints](/docs/workload-protection?topic=workload-protection-supported-regions#endpoints_ingestion).

6. Install the kernel headers for your distribution if they are missing:

   - For Debian and Ubuntu:

     ```sh
     apt-get -y install linux-headers-$(uname -r)
     ```
     {: pre}

   - For RHEL, CentOS, and Fedora:

     ```sh
     yum -y install kernel-devel-$(uname -r)
     ```
     {: pre}

7. If you are using the `universal_ebpf` driver, confirm that the host kernel version is 5.8 or later:

   ```sh
   uname -r
   ```
   {: pre}

   If the kernel version is earlier than 5.8, switch to a supported driver type or upgrade the kernel.

      The `universal_ebpf` driver requires kernel version 5.8 or newer. If you have a lower version you need BPF ring buffer support and a kernel that exposes BTF (BPF Type Format). If you have any problem during the agent installation, try removing the lines `agent.ebpf.enabled: true` and `agent.ebpf.kind: universal_ebpf` or [contact support](/docs/workload-protection?topic=workload-protection-gettinghelp).
   {: note}

   For more information, see [Managing the {{site.data.keyword.sysdigsecure_short}} agent on Linux](/docs/workload-protection?topic=workload-protection-manage-linux-agent).
