---

title : "Security"

date : "`r Sys.Date()`"

weight : 4

chapter : false

pre : " <b> 5.4 </b> "

---

### Overview

After building the infrastructure and automation environment, the project implements several **Security** functions to protect and verify the security status of the Managed Nodes.

The main security functions implemented in the project are **SSH Hardening**, **Firewall**, and **Security Audit**.

Among these components, SSH Hardening and Firewall are implemented through Ansible, while Security Audit is used to verify the security configurations applied to the Managed Nodes.

### Main Security Components

~~~text
Security

├── SSH Hardening
│   └── Secure SSH configuration
│
├── Firewall
│   └── Control network traffic
│
└── Security Audit
    └── Verify security configuration
~~~

### Security Workflow

The overall security workflow is:

~~~text
Managed Nodes

      ↓

SSH Hardening + Firewall

      ↓

Security Audit

      ↓

Security Status

      ↓

Python Security Engine
~~~

Ansible is responsible for applying and checking security configurations, while the Python Security Engine will process the collected security information in the following sections.

### Workshop Sections

+ [5.4.1 SSH Hardening]({{< relref "5.4.1-SSH-hardening">}})

+ [5.4.2 Firewall]({{< relref "5.4.2-firewall">}})

+ [5.4.3 Security Audit]({{< relref "5.4.3-Security-Audit">}})