# 🛡️ Elastic Agent Deployment for Security Onion

![Security Onion Logo][logo]

[logo]:https://private-user-images.githubusercontent.com/127058080/353984634-bea2f232-053c-429e-8910-89ba34560917.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjI0NTc4NTQsIm5iZiI6MTcyMjQ1NzU1NCwicGF0aCI6Ii8xMjcwNTgwODAvMzUzOTg0NjM0LWJlYTJmMjMyLTA1M2MtNDI5ZS04OTEwLTg5YmEzNDU2MDkxNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzMxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDczMVQyMDI1NTRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0zMjYwYWFiYmE2OWViYzZhNmU5NjU2OTI4YzA0NmYxYWQ4YTQxYzNkYTA2ZDUwMzgzMjk3NTU4YmE2NWI1ODA5JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9._-oggnecmhBv0FWWjSxyXVFPaVsDtKrQrC8t2-E8KoU "Security Onion Logo"

This repository contains Ansible playbooks for deploying Elastic Agents in Elastic Fleet, tailored specifically for Security Onion environments. Our playbooks streamline the installation, configuration, and management of Elastic Agents across multiple endpoints, ensuring seamless integration with Security Onion's threat hunting and network security monitoring capabilities.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Ansible Version](https://img.shields.io/badge/Ansible-2.9+-green.svg)](https://www.ansible.com/)

---

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Repository Structure](#repository-structure)
- [Detailed Usage](#detailed-usage)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)

---

## 🔧 Prerequisites

Before you begin, ensure you have:

- Ansible 2.9 or higher installed on your control node
- SSH access to target hosts
- Elastic Fleet server configured in your Security Onion setup

---

## 📁 Repository Structure


- `Os_based_deployment.yaml`: Main Ansible playbook for deploying Elastic Agents
- `inventory.ini`: Inventory file listing target hosts

---
## 📘 Detailed Usage

### Preparing Your Environment

1. Ensure your Elastic Fleet server is properly configured in Security Onion.

2. Verify SSH access to all target hosts.

3. Update the `inventory.ini` file:
```
[windows]
win_host1 ansible_host=192.168.1.101
win_host2 ansible_host=192.168.1.102

[linux]
linux_host1 ansible_host=192.168.1.201
linux_host2 ansible_host=192.168.1.202
Running the Playbook
Execute the playbook with the following command:
┌───────────────────────────────────────────────────────────┐
│ ansible-playbook -i inventory.ini Os_based_deployment.yaml│ 
└───────────────────────────────────────────────────────────┘
This will start the deployment process across all specified hosts.
Show Image
Verifying Deployment
After running the playbook:

Check the Elastic Fleet server to confirm new agents are connected.
Verify data flow in Security Onion's Kibana interface.
---
## 🔧 Customization

Modifying the Playbook

Open the Os_based_deployment.yaml file in your preferred text editor.
Locate the following sections to customize:
yamlCopyvars:
  agent_version: "8.2.0"
  fleet_url: "https://your-fleet-server:8220"
  # Add more variables as needed

Adjust the variables according to your requirements:

Update agent_version to your desired Elastic Agent version
Modify fleet_url to match your Fleet server address



Customizing for Different OS Types

In the Os_based_deployment.yaml file, find the OS-specific tasks:
yamlCopy- name: Install Elastic Agent on Windows
  win_shell: # Windows-specific commands
  when: ansible_os_family == "Windows"

- name: Install Elastic Agent on Linux
  shell: # Linux-specific commands
  when: ansible_os_family == "Linux"

Adjust the commands and conditions as needed for your environment.

Adding New Integration Options

To add a new integration, append to the integrations list in the playbook:
yamlCopyvars:
  integrations:
    - name: "system"
    - name: "auditd"
    # Add your new integration here
    - name: "your_new_integration"

Ensure the corresponding integration is available in your Fleet server.

🆘 Troubleshooting
SSH Connection Failures


Verify SSH key configuration:
┌─────────────────────────────────────────────┐
│ ssh-copy-id user@target_host                │
└─────────────────────────────────────────────┘

Check firewall settings on target hosts:

For Linux:
┌─────────────────────────────────────────────┐
│ sudo iptables -L                            │
└─────────────────────────────────────────────┘

For Windows, check Windows Firewall settings in the Control Panel


Test network connectivity:
┌─────────────────────────────────────────────┐
│ ping target_host                            │
└─────────────────────────────────────────────┘


Agent Registration Errors

Confirm Fleet server URL:

Open Os_based_deployment.yaml
Verify the fleet_url variable is correct


Check enrollment tokens:

Log into your Fleet server
Navigate to Fleet > Enrollment Tokens
Ensure the token in your playbook matches an active token


Verify outbound connectivity:
┌─────────────────────────────────────────────┐
│ curl -v https://your-fleet-server:8220      │
└─────────────────────────────────────────────┘


Debugging the Playbook
To get more information during playbook execution, use the -vvv flag:
┌──────────────────────────────────────────────────────────────────┐
│ ansible-playbook -i inventory.ini Os_based_deployment.yaml -vvv  │
└──────────────────────────────────────────────────────────────────┘
---
