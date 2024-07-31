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
- [Quick Start](#quick-start)
- [Detailed Usage](#detailed-usage)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

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

## 🚀 Quick Start

1. Clone this repository:
┌────────────────────────────────────────────────────────────────────────────┐
 git clone https://github.com/yourusername/elastic-agent-security-onion.git                   
└────────────────────────────────────────────────────────────────────────────┘
┌────────────────────────────────────────────────────────────────────────────┐
 cd elastic-agent-security-onion                                        
└────────────────────────────────────────────────────────────────────────────┘

3. Update the `inventory.ini` file with your target hosts.

4. Run the playbook:
┌────────────────────────────────────────────────────────────┐
│ ansible-playbook -i inventory.ini Os_based_deployment.yaml │
└────────────────────────────────────────────────────────────┘

---

## 📘 Detailed Usage

### Preparing Your Environment

1. Ensure your Elastic Fleet server is properly configured in Security Onion.

2. Verify SSH access to all target hosts.

3. Update the `inventory.ini` file:
```ini
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


🔧 Customization
To customize the deployment for your environment:

Edit Os_based_deployment.yaml to modify:

Agent versions
Configuration settings
Integration options


Adjust variables for different OS types or host groups.


🆘 Troubleshooting
Common issues and solutions:
<details>
<summary>SSH Connection Failures</summary>

Ensure SSH keys are properly set up
Check firewall settings on target hosts
Verify network connectivity

</details>
<details>
<summary>Agent Registration Errors</summary>

Confirm Fleet server URL is correct
Check enrollment tokens
Verify outbound connectivity from agents to Fleet server

</details>

🤝 Contributing
We welcome contributions! Please follow these steps:

Fork the repository
Create a new branch:
┌─────────────────────────────────────────┐
│ git checkout -b feature-branch-name     │ 
└─────────────────────────────────────────┘

Make your changes and commit them:
┌─────────────────────────────────────────┐
│ git commit -m 'Add some feature'        │
└─────────────────────────────────────────┘

Push to the branch:
┌─────────────────────────────────────────┐
│ git push origin feature-branch-name     │
└─────────────────────────────────────────┘

Submit a pull request


📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

<p align="center">
  Made with ❤️ by Your Team Name
</p>
```
