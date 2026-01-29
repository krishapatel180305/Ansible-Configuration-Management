# Ansible-Configuration-Management
Automating Nginx installation and configuration using Ansible on AWS.

**Ansible Configuration Management: Automated Nginx Deployment**

# Project Overview
This project demonstrates how to use **Ansible** for automated configuration and software deployment on AWS EC2 instances. The goal was to eliminate manual steps by using a central Control Node to manage a remote Target Server.

# Infrastructure Setup
- **Cloud Provider**: AWS
- **Instances**: 2 x Amazon Linux 2023 (t2.micro)
- **Control Node**: Host where Ansible is installed.
- **Target Server**: Remote node where Nginx is deployed.
- **Security**: Port 22 (SSH) enabled for communication.

# Implementation Details

**1. SSH Key Management**
- Generated RSA key pair on the Control Node.
- Configured passwordless SSH by sharing the public key with the Target Server's `authorized_keys`.

**2. Configuration & Automation**
- **Inventory (`hosts`)**: Defined the target IP and connection parameters.
- **Playbook (`setup_nginx.yml`)**: Created a YAML script to:
    - Update the system and install the Nginx package.
    - Start the Nginx service.
    - Enable the service to ensure it starts automatically after a reboot.

## Troubleshooting & Learnings
- **Auth Issue**: Resolved `Permission denied (publickey)` by mapping the `ec2-user` identity in the inventory.
- **Service State**: Fixed an issue where Nginx was installed but "inactive" by adding a dedicated service management task.
- **Connectivity**: Managed SSH fingerprints manually to establish a trusted handshake.

## Results
- **Success Rate**: 100% Automation achieved.
- **Verification**: Service status confirmed as `active (running)` on the remote host.
- **Outcome**: Successfully served the default Nginx page via the remote server's IP.
