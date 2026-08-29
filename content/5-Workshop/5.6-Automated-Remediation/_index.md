---

title : "Automated Remediation"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 5.6 </b> "
----------------------

### Overview

After the system performs **Security Checks** and identifies security issues, the next step is **Remediation**.

In this project, the Remediation function is implemented as part of the Python Security Engine and works together with Ansible.

The main component related to Remediation is:

```text
python/
└── security_engine/
    └── remediation.py
```

Ansible is responsible for executing the required configuration changes on the Managed Nodes.

### 1. Role of Automated Remediation

Automated Remediation is used to address security issues detected during the Security Audit process without requiring administrators to perform each step manually.

The general workflow is:

```text
Security Check
      |
      ↓
   Finding
      |
      ↓
 Remediation
      |
      ↓
   Ansible
      |
      ↓
Managed Nodes
      |
      ↓
   Verify
```

This creates a closed-loop process from detecting a security issue to remediating and verifying it.

### 2. remediation.py

File:

```text
python/security_engine/remediation.py
```

is the component responsible for the Remediation process within the Python Security Engine.

It connects the Finding stage with the execution of changes on the Managed Nodes.

```text
Finding
   |
   ↓
remediation.py
   |
   ↓
Ansible
   |
   ↓
Managed Node
```

![ASAU](/images/01/image_262.png)

![ASAU](/images/01/image_263.png)

![ASAU](/images/01/image_264.png)

### 3. Integration Between Python and Ansible

Python and Ansible have different responsibilities in the project.

```text
Python
  |
  | Analysis / Decision
  ↓
Remediation
  |
  | Trigger Automation
  ↓
Ansible
  |
  | Apply Changes
  ↓
Managed Nodes
```

Python is responsible for the Security Engine logic, while Ansible provides the automation mechanism used to apply configuration changes on the Managed Nodes.

### 4. Detect → Remediate → Verify

Automated Remediation can be described through three main stages:

```text
Detect
  ↓
Finding
  ↓
Remediate
  ↓
Managed Node
  ↓
Verify
  ↓
Security Status
```

#### Detect

Security Checks inspect the state of the Managed Nodes and generate a Finding when a security issue is detected.

#### Remediate

The Security Engine determines how the Finding should be handled and performs the remediation through the project's automation mechanism.

#### Verify

After remediation is completed, the system checks the state again to determine whether the identified issue has been resolved.

![ASAU](/images/01/image_265.png)

### 5. Relationship with Security Policy

Security Policy provides the criteria used by the system to evaluate the security state.

```text
Security Policy
      |
      ↓
Security Checks
      |
      ↓
   Finding
      |
      ↓
Remediation
      |
      ↓
Managed Nodes
```

This ensures that the remediation process aims to bring the Managed Nodes back to a state that complies with the project's security policy.

### 6. Relationship with Ansible Playbooks

Ansible acts as the automation execution layer.

```text
Python Security Engine
          |
          ↓
      Remediation
          |
          ↓
       Ansible
          |
          ↓
    Playbook / Role
          |
          ↓
    Managed Nodes
```

Playbooks and Roles perform the required changes on the servers according to the project's design.

### 7. Overall Workflow

The overall Automated Remediation workflow is:

```text
Managed Nodes
      |
      ↓
Security Checks
      |
      ↓
   Finding
      |
      ↓
Security Engine
      |
      ↓
remediation.py
      |
      ↓
   Ansible
      |
      ↓
Managed Nodes
      |
      ↓
   Verify
      |
      ↓
Updated State
```

This process creates the following loop:

```text
Detect → Remediate → Verify
```

The state after verification can then be stored in the Security State or included in the generated Report.

### 8. Result

After implementing Automated Remediation, the project can establish an automated security management workflow:

```text
Security Audit
      ↓
Detect Finding
      ↓
Remediation
      ↓
Ansible
      ↓
Managed Node
      ↓
Verify
      ↓
Report / State
```

An important aspect of this architecture is that **Python does not replace Ansible**. Instead, Python processes the Security Engine logic and works together with Ansible to perform automation on the Managed Nodes.
