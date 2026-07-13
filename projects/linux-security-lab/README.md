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

**Why it matters:** Outdated packages may contain known vulnerabilities (CVEs) that have already been patched upstream. Applying updates is the first step in any hardening process, as it addresses software-level flaws that no manual configuration can fix.

---

### 2. User Account Review

**Baseline:**
Reviewed all system accounts using `cat /etc/passwd` to identify which accounts had login-capable shells versus system/service accounts.

- All service accounts (e.g., `daemon`, `bin`, `www-data`) were correctly configured with `/usr/sbin/nologin` or `/bin/false`, preventing interactive login.
- One exception was noted: the `sync` account uses `/bin/sync`, which is standard, well-documented Unix/Linux behavior (allows forcing a disk write from the login prompt without authentication) and does not represent a misconfiguration.
- Verified administrative privileges using `getent group sudo` — only the intended administrator account was a member of the `sudo` group, with no unnecessary or unexpected accounts holding elevated privileges.

**Remediation:**
No remediation was required. All accounts were found to be correctly configured at first boot, following the principle of least privilege.

**Verification:**
Findings were confirmed by directly inspecting command output (`/etc/passwd` and `getent group sudo`) rather than relying on default assumptions.

**Why it matters:** Reviewing user accounts — even when no issues are found — establishes a documented baseline for account governance. It confirms that service accounts cannot be used as an entry point for unauthorized login, and that administrative access is limited to the intended personnel, reducing the attack surface from the start.

---

### 3. SSH Hardening

**Baseline:**
After installing OpenSSH server (intentionally not installed during OS setup, to allow full manual configuration and documentation), the default configuration was reviewed using:
```bash
sudo cat /etc/ssh/sshd_config | grep -E "PermitRootLogin|PasswordAuthentication|Port"
```

Findings:
| Setting | Default Value | Risk |
|---|---|---|
| `Port` | 22 (commented, using internal default) | Low — increases exposure to automated bot scans |
| `PermitRootLogin` | `prohibit-password` (commented, using internal default) | Medium — root login still possible via key |
| `PasswordAuthentication` | `yes` (commented, using internal default) | High — allows brute-force login attempts |

Given the organization's remote workforce, password-based SSH authentication was identified as the highest-priority risk, as it directly exposes the server to automated brute-force attacks over the internet.

**Remediation:**

1. Generated a dedicated SSH key pair (Ed25519) on the client machine, protected with a passphrase:
```bash
ssh-keygen -t ed25519 -C "northwind-admin-key" -f ~/.ssh/northwind_server_key
```

2. Copied the public key to the server and confirmed key-based login worked *before* disabling password authentication (to avoid lockout):
```bash
ssh-copy-id -i ~/.ssh/northwind_server_key.pub -p 2222 mboyanv@localhost
ssh -i ~/.ssh/northwind_server_key -p 2222 mboyanv@localhost
```

3. Edited `/etc/ssh/sshd_config` and applied the following changes:

PasswordAuthentication no
PermitRootLogin no
Port 2200

4. Updated VirtualBox NAT port forwarding to map host port 2222 → guest port 2200 (previously mapped to port 22), to stay consistent with the new internal SSH port.

**Issue encountered:** After updating the `Port` directive, SSH continued listening on port 22 instead of 2200.

**Root cause:** Ubuntu 24.04 uses systemd socket activation (`ssh.socket`) to manage the SSH listening port independently of `sshd_config`. The socket unit remained bound to port 22, overriding the configuration file.

**Resolution:**
```bash
sudo systemctl disable --now ssh.socket
sudo systemctl enable --now ssh.service
sudo systemctl restart ssh.service
```

**Verification:**
- Confirmed via `ss -tlnp | grep ssh` that `sshd` was listening on port 2200 with a new process ID, confirming the configuration reload.
- Confirmed key-based authentication works:
```bash
ssh -i ~/.ssh/northwind_server_key -p 2222 mboyanv@localhost
```
- Confirmed password authentication is fully disabled by attempting connection without specifying the key:
```bash
ssh -p 2222 mboyanv@localhost
# Result: Permission denied (publickey)
```

**Why it matters:** With remote employees requiring SSH access, password-based authentication represents a direct and continuously exploitable attack vector, as automated bots constantly scan the internet for exposed SSH services. Enforcing key-based authentication eliminates brute-force risk entirely, disabling root login removes the highest-privilege target from remote access, and moving off the default port reduces exposure to opportunistic automated scanning — a reasonable trade-off for a small organization where remembering a non-standard port is operationally manageable.

---
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
