# Windows Server 2022: **Patch Management Fundamentals & Action1**

## Part 1: Patch Management Concepts

### What Is Patch Management?

The process of identifying, testing, deploying, and tracking software updates (patches) across systems to fix bugs, close security vulnerabilities, and maintain compliance.

### Common Patch Management Tools

| Tool | Notes |
| --- | --- |
| **Action1** | Free tier; used in this lab |
| NinjaOne | Commercial RMM |
| PDQ | Commercial deployment tool |
| SSCM (SCCM/MECM) | Microsoft enterprise tool |
| ManageEngine | Commercial suite |

### Why Patch Management Matters

- **Security** — fixes bugs and vulnerabilities (CVEs)
- **Compliance** — required for audits and regulatory frameworks
- **System stability** — reduces crashes and compatibility issues
- **New features** — keeps software current

### Key Security & Compliance Frameworks

- **SOC 2 Type 2** — trust services criteria audit
- **PCI DSS** — payment card industry standard
- **ISO 27001** — information security management standard
- **HIPAA** — healthcare data protection (US)

---

## Part 2: Patch Management Best Practices

### Timing

- Schedule patching **outside business hours**.
- Avoid disrupting users, especially executives who work during market hours.
- **Avoid updates that require reboots** during the workday , Windows updates in particular may force restarts.

Patch management programs involve:

- Scanning systems
- Testing patches
- Deploying patches
- Tracking and **auditing** results

> Failing an audit is a serious outcome, always with reports.
> 

---

## Part 3: Hands-On Installing the Action1 Agent

<img width="1010" height="567" alt="image" src="https://github.com/user-attachments/assets/cfbada60-3547-451e-8ace-576d1a197533" />

1. Log into the free **Action1** dashboard.
2. Download the **agent MSI** installer.
3. On the target VM, place the installer in a known folder
4. Run the installer → **Next → Next → Install**.
5. The agent **requires internet access** to register. If the VM is on a host-only network, temporarily enable the NAT/bridged adapter in VirtualBox (Devices → Network → Bridged Adapter) or restore internet in TCP/IPv4 settings.
6. Refresh the Action1 dashboard,  the endpoint should appear with status **Connected**.

### Agent Capabilities (from dashboard)

- Deploy software
- Deploy updates
- Reboot
- Run scripts
- Uninstall software
- Remote desktop

---

## Part 4: Deploying Updates via Action1

1. In the dashboard, view **missing updates** for the endpoint (e.g., domain controller missing updates).
2. Select the updates → **Deploy updates**.
3. Configure options:
    - **Automatically reboot if required** , enabled
    - **Manage timeout** , 1 hour
4. Choose scheduling: run now, specific day, every time, or weekly. Select **Run now**.
5. Monitor status: *"Waiting for endpoint to run automation"* → *"Running"*.
6. On the endpoint, the agent installer runs and updates begin installing

---

## Part 5: Generating Audit & Compliance Reports

Action1 provides **built-in reports** useful for auditors and management.

### Accessing Reports

Dashboard → **Reports** → **Built-in reports** (custom reports available too).

### Useful Report Types

| Report | Purpose |
| --- | --- |
| **Vulnerability management** | Show patching of CVEs and document controls |
| **Endpoint inventory** | List all managed assets (count, last seen, OS, agent ID) |
| **Hardware inventory** | Motherboard, physical memory, hardware summary |
| **Software inventory** | Installed applications per machine |
| **Patch management** | Latest CVEs, Windows critical updates applied |

### Exporting for Auditors

1. Open a report (e.g., endpoint inventory).
2. Right-click → **Print** → **Save as PDF**.
3. Save to a folder (e.g., `Audits`).
4. Email to the auditor.
