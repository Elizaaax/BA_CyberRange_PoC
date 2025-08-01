# Modular Cyber Range PoC – Web Pentesting Scenario Framework

This repository contains a modular, role-based automation project for simulating adversarial behavior in web-based penetration testing scenarios.  
It is the technical foundation of the Bachelor thesis _“Developing a Modular Concept for Realistic Cyber Range Scenarios for Web Pentesting”_ (2025).

> Based on Ansible and full virtualization, this project enables the orchestration and execution of composable attack chains following the FASAC model and MITRE ATT&CK mapping.

---

## Repository Structure

```
BA_CyberRange_PoC/
├── group_vars/
│   └── all.yml                  # Global IP and scenario variable definitions
├── roles/
│   ├── setup-*                  # Infrastructure provisioning roles
│   ├── poc1/                    # PoC 1 scenario (system-level compromise)
│   ├── poc2/                    # PoC 2 scenario (web/session-based attack)
│   └── chain/                   # Hybrid Chain Scenario
├── ansible.cfg
├── inventory.ini
└── site.yml                     # Entry playbook
```

---

## Setup Roles (Infrastructure Preparation)

Each virtual machine is prepared using a dedicated Ansible role:

| Role | Description |
|------|-------------|
| `setup-attacker` | Installs offensive tools like `nmap`, `sqlmap`, `curl`, etc. |
| `setup-web-victim` | Deploys DVWA, Apache, PHP, and XSS/vulnerability settings |
| `setup-privesc-target` | Enables weak privilege escalation vectors (e.g. SUID) |
| `setup-collector` | Sets up a passive HTTP/TCP listener for exfiltrated data |

To provision the full environment:

```bash
ansible-playbook -i inventory.ini site.yml --tags "setup"
```

> ℹ️ All static IPs and system roles are defined in `group_vars/all.yml`

---

## Scenario Roles

The following scenarios are implemented as modular roles:

### PoC 1 – Operation Silent Upload

System-level attack involving:
- File upload exploitation (DVWA)
- Remote shell
- SSH lateral movement
- Privilege escalation (SUID)
- Reverse shell & file exfiltration

```bash
ansible-playbook -i inventory.ini site.yml --tags "poc1"
```

---

### PoC 2 – Operation Cookie Harvest

Application-level attack:
- Stored XSS
- JavaScript-based session cookie theft
- Session hijacking via replay
- Access to admin resources

```bash
ansible-playbook -i inventory.ini site.yml --tags "poc2"
```

---

### 🔁 PoC 3 – Hybrid Chain Scenario

**Manual execution only.**  
Combines PoC 1 and PoC 2 into a hybrid attack chain:
- Branch A: File upload → SSH pivot → root access
- Branch B: XSS → cookie theft → impersonation
- Converges into shared exfiltration phase

> This hybrid attack was manually orchestrated based on existing modular roles.  
> It demonstrates the **chaining capability** and interoperability of isolated scenario phases.

---

## ⚙Configuration

The `group_vars/all.yml` defines key variables such as:

```yaml
attacker_ip: "192.168.254.129"
web_victim_ip: "192.168.254.130"
privesc_target_ip: "192.168.254.131"
collector_ip: "192.168.254.132"

active_scenario: "poc1"     # Change to "poc2" or "chain" as needed
```

---

## Related Bachelor Thesis

The underlying architecture, scenario model, and framework were developed as part of the following thesis:

> **Zarei, E. (2025).**  
> _Developing a Modular Concept for Realistic Cyber Range Scenarios for Web Pentesting_  
> Universität der Bundeswehr München

You can cite or reference the full thesis and implementation details accordingly.

---

## License

This project is for educational and research use only.  
No real-world exploitation or illegal use is permitted.

MIT License © Elaheh Zarei
