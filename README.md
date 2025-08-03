```markdown
# 🛡️ BA_CyberRange_PoC

## ⚠️ **CRITICAL SECURITY WARNING** ⚠️

**🚨 FOR EDUCATIONAL PURPOSES ONLY - USE AT YOUR OWN RISK 🚨**

This repository contains **REAL ATTACK TECHNIQUES** and **FUNCTIONAL MALWARE COMPONENTS** including:
- **PHP Webshells** that execute arbitrary commands
- **Privilege Escalation Exploits** using real SUID techniques
- **Persistent Backdoors** via cron jobs and reverse shells
- **Data Exfiltration** mechanisms

**⚠️ IMPORTANT:**
- **NEVER** use this in production environments
- **NEVER** run against systems you don't own
- **ALWAYS** use in isolated, controlled environments
- **ALWAYS** follow responsible disclosure practices
- **ALWAYS** ensure proper cleanup after testing

This repository contains the implementation of three modular proof-of-concept (PoC) scenarios developed as part of the bachelor's thesis _"Developing a Modular Concept for Realistic Cyber Range Scenarios for Web Pentesting"_. The scenarios are designed using role-based virtualization, Infrastructure-as-Code principles, and reusable attack phases modeled after the FASAC framework.

---

## Repository Structure

```

├── .gitignore                   # Git ignore patterns
├── group\_vars/                 # Central variables (IP addresses, toggles, credentials)
├── site.yml                     # Central playbook to launch setup or PoC chains
├── roles/
│   ├── setup-attacker/          # Attacker machine provisioning
│   ├── setup-web-victim/        # DVWA setup and web-layer configuration
│   ├── setup-privesc-target/    # SUID privilege escalation target
│   ├── setup-collector/         # Data exfiltration sink
│   ├── poc1/                    # Operation Silent Upload
│   ├── poc2/                    # Operation Cookie Harvest
│   └── poc3/                    # Hybrid Chain Scenario

````

---

## Overview of Scenarios

| PoC | Name                      | Focus                         | MITRE Tactics Covered                                 |
|-----|---------------------------|-------------------------------|-------------------------------------------------------|
| 1   | Operation Silent Upload   | File upload, privesc, exfil   | Initial Access, Escalation, Persistence, Exfiltration |
| 2   | Operation Cookie Harvest  | Stored XSS, session hijack    | Execution, Credential Access, C2                      |
| 3   | Hybrid Chain Scenario     | Combined PoC1 + PoC2          | All of the above                                      |

Each PoC is built from reusable roles, separated by adversarial phase:
- `reconnaissance`
- `initial-access`
- `privilege-escalation`
- `persistence`
- `action-on-objectives`

---

## Getting Started

### ✅ Prerequisites
- **Ansible** ≥ 2.10
- **Python** ≥ 3.6 (for optional tools)
- Local hypervisor (e.g., VirtualBox) with 4 VMs:
  - `deb-attacker` (192.168.254.130)
  - `deb-web-victim` (192.168.254.129)
  - `deb-privesc-target` (192.168.254.132)
  - `deb-collector` (192.168.254.131)

### 🔧 Installation
```bash
# Clone the repository
git clone https://github.com/elizaaax/BA_CyberRange_PoC.git
cd BA_CyberRange_PoC
```

### Provision the Environment
```bash
# Run all setup tasks
ansible-playbook site.yml --tags "setup"

# Or run without tags to execute everything
ansible-playbook site.yml
````

### ▶Run PoC 1 or 2

```bash
# PoC 1: Operation Silent Upload
ansible-playbook site.yml -e run_poc1=true -e poc1_phases='["reconnaissance", "initial-access", "privilege-escalation", "persistence", "action-on-objectives"]'

# PoC 2: Operation Cookie Harvest
ansible-playbook site.yml -e run_poc2=true -e poc2_phases='["reconnaissance", "initial-access", "privilege-escalation", "persistence", "action-on-objectives"]'
```

### Run PoC 3 (Hybrid Chain)

```bash
# Run PoC3 with all phases
ansible-playbook site.yml -e run_poc3=true

# Run PoC3 with specific phases
ansible-playbook site.yml -e run_poc3=true -e poc3_phases='["reconnaissance", "initial-access", "privilege-escalation", "persistence", "action-on-objectives"]'
```

---

## 🎯 Features

- **Modular Design**: Reusable attack phases across different scenarios
- **Infrastructure as Code**: Complete automation with Ansible
- **Educational Focus**: Designed for learning web penetration testing
- **Professional Standards**: Follows Ansible best practices
- **Error Handling**: Robust execution with proper error handling
- **Variable Management**: Centralized configuration for easy customization

## 🔒 Security Notice

⚠️ **For Educational Purposes Only**
- This project is designed for educational and research environments
- Use only in isolated, controlled environments
- Follow responsible disclosure practices
- All credentials are intentionally weak for demonstration purposes

---

## Research Background

This implementation supports the modular cyber range design described in the following thesis:

> Zarei, E. (2025). *Developing a Modular Concept for Realistic Cyber Range Scenarios for Web Pentesting*. Universität der Bundeswehr München.

The system architecture and scenario design are based on the FASAC model (Scenario, Attack Chain, System, Execution). PoC scenarios are mapped to real-world MITRE ATT\&CK techniques and validated in a virtual, Ansible-automated environment.

---

## Related Work and Resources

* [MITRE ATT\&CK Matrix](https://attack.mitre.org/)
* [DVWA – Damn Vulnerable Web Application](http://www.dvwa.co.uk/)
* [Ansible Best Practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html)
* [FASAC Framework](https://www.researchgate.net/publication/example) - Framework for Attack Scenario Analysis and Classification

## 📝 License

This project is licensed for academic and research purposes. Contact [@elizaaax](https://github.com/elizaaax) for more details.

```