---

title : "Workshop"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---------------------

### Overview

In this project, we build an **Enterprise Infrastructure Automation** system to automate the deployment, configuration, security assessment, and management of Linux servers.

The project uses **Amazon Web Services (AWS)** to provide the infrastructure environment, **Ansible** for configuration management and automation, and **Python** to build a Security Engine for security checking and assessment.

The deployment environment consists of one **Automation Server** and two **Managed Nodes**. The Automation Server acts as the central control node, while Managed-Node-01 and Managed-Node-02 are the servers managed through Ansible.

### Overall Architecture

The project architecture is organized as follows:

```text
                    AWS VPC
                   10.0.0.0/16
                        |
          +-------------+-------------+
          |                           |
    Public Subnet               Private Subnet
     10.0.1.0/24                 10.0.2.0/24
          |                           |
          |                    +------+------+
          |                    |             |
   Automation Server     Managed-Node-01  Managed-Node-02
          |
     Ansible + Python
```

The Automation Server is deployed in the **Public Subnet** and acts as the control server. The two Managed Nodes are deployed in the **Private Subnet** and are centrally managed by the Automation Server.

This architecture separates the control server from the managed servers and reduces the need to directly expose the Managed Nodes to the Internet.

<!--
Insert image: Overall project architecture diagram.

The diagram should show the AWS VPC, Public/Private Subnets,
Automation Server, and the two Managed Nodes.
-->

### Technologies Used

The project uses the following main components:

| Component | Role                                                                  |
| --------- | --------------------------------------------------------------------- |
| AWS VPC   | Provides the network environment for the project                      |
| AWS EC2   | Provides Linux servers                                                |
| Ansible   | Configuration management and automation                               |
| Python    | Implements the Security Engine                                        |
| SSH       | Provides connectivity between the Automation Server and Managed Nodes |
| Git       | Source code management                                                |

The EC2 instances in the project use **Ubuntu Server 24.04 LTS**. The Automation Server is configured to run Ansible and Python, while the two Managed Nodes are placed in the Private Subnet for centralized management.

### Workflow

The overall system workflow consists of the following main stages:

```text
AWS Infrastructure
        ↓
Automation Server
        ↓
SSH Connectivity
        ↓
Ansible Automation
        ↓
Security Hardening
        ↓
Security Audit
        ↓
Python Security Engine
        ↓
Automated Remediation
        ↓
Verification
```

First, AWS is used to build the network infrastructure and EC2 instances. The Automation Server is then prepared with Python and Ansible.

Next, SSH connectivity is established between the Automation Server and the Managed Nodes. Ansible is used to manage system configurations, perform security hardening, and support security status checks.

The Python Security Engine then processes security information, performs Security Checks, and generates Security Findings. When a security issue is detected, Ansible is used to perform remediation. The system then performs verification to confirm the resulting security state.

### Workshop Contents

The Workshop is divided into the following main sections:

* **AWS Infrastructure** — Build the VPC, Subnets, Internet Gateway, Route Tables, Security Groups, and EC2 instances.

* **Automation Server** — Prepare the Python and Ansible environment.

* **SSH Connectivity** — Establish connectivity between the Automation Server and Managed Nodes.

* **Ansible Automation** — Build the Inventory, Playbooks, and Roles.

* **Security** — Implement SSH Hardening, Firewall, and Security Audit.

* **Python Security Engine** — Build Security Checks, Security Engine, and Reporting.

* **Automated Remediation** — Detect, remediate, and verify security issues.

* **Project Validation** — Validate the complete system workflow.

The following sections will implement each component step by step, starting with the AWS infrastructure, followed by the Automation Server, SSH connectivity, Ansible Automation, Security functions, Python Security Engine, and Automated Remediation.
