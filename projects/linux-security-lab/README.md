# Linux Server Hardening & Access Control Assessment – Northwind Health Services

## Scenario
Northwind Health Services is a healthcare company with approximately 80 employees. The organization operates an Ubuntu server that hosts an internal web application and files containing patient information (PII/SPII). The company has remote employees who connect to internal systems, and has never had a dedicated security specialist on staff.

With an upcoming security audit, Northwind hired a Junior Security Analyst to assess and reduce risk across the server environment — not by deploying complex security tools, but by applying fundamental hardening practices appropriate for a small organization's first security review.

## Objective
To perform a baseline security assessment of a newly provisioned Ubuntu Server, identify configuration weaknesses across user accounts, SSH access, firewall rules, and sensitive file permissions, and apply hardening measures aligned with CIS Benchmark principles — while documenting the reasoning behind each decision.

## Scope
- System updates and patch management
- User account review and privilege management
- SSH access hardening
- Firewall configuration (UFW)
- Sensitive file permissions (simulated patient data)

## Lab Environment
- **Hypervisor:** Oracle VirtualBox 7.0.x (selected for compatibility with macOS Big Sur 11.7)
- **Guest OS:** Ubuntu Server 24.04.4 LTS
- **Host:** MacBook (Intel), 16GB RAM
- **VM Resources:** 4096 MB RAM, 2 vCPUs, 25GB dynamically allocated disk
- **Network:** NAT (default), to be reconfigured for SSH access testing

## Methodology
This assessment follows a four-phase approach:
1. **Baseline Assessment** – Document the current state of the system before any changes.
2. **Remediation** – Apply configuration changes to address identified gaps.
3. **Verification** – Confirm each change was applied successfully.
4. **Documentation** – Record before/after state, commands used, and justification for each control.

## Findings & Remediation Log

### 1. System Updates
**Baseline:** Upon first boot, the system had multiple outdated packages pending update, confirmed via `apt list --upgradable`.

**Remediation:**
```bash
sudo apt update
sudo apt upgrade -y
```

**Verification:** Confirmed via `ls /var/run/reboot-required` — no reboot required after upgrade.

Upon first boot, the system had multiple outdated packages pending updates, confirmed via apt list --upgradable. All packages were updated using apt update && apt upgrade -y, with no reboot required afterward.

**Why it matters:** Outdated packages may contain known vulnerabilities (CVEs) that have already been patched upstream. Applying updates is the first step in any hardening process, as it addresses software-level flaws that no manual configuration can fix.

---

### 2. User Account Review
*(pending)*

### 3. SSH Hardening
*(pending)*

### 4. Firewall Configuration
*(pending)*

### 5. Sensitive File Permissions
*(pending)*

## Skills Demonstrated
*(to be completed at the end)*

## Tools & Frameworks
- CIS Benchmark principles (Ubuntu Linux)
- Oracle VirtualBox
- Ubuntu Server 24.04 LTS
