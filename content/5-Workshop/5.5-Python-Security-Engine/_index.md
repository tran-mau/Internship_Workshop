---

title : "Python Security Engine"

date : "`r Sys.Date()`"

weight : 5

chapter : false

pre : " <b> 5.5 </b> "

---

### Overview

- **Python Security Engine** is the component responsible for handling the security logic of the project. While Ansible focuses on automation and configuration management, Python is responsible for performing **Security Checks**, processing **Findings**, managing security state, generating reports, and supporting the **Remediation** process.

- Python Security Engine works together with Ansible to create an automated security workflow. Python is responsible for security processing and analysis logic, while Ansible is responsible for executing configuration changes on the Managed Nodes.

### Workshop Sections

+ [5.5.1 Python Security Engine Architecture]({{< relref "5.5.1-Python-SE-Structure">}})

+ [5.5.2 Security Checks]({{< relref "5.5.2-Security-Check">}})

+ [5.5.3 Security Engine]({{< relref "5.5.3-Security-Engine">}})

+ [5.5.4 Finding and State]({{< relref "5.5.4-Finding-State">}})

+ [5.5.5 Reporting]({{< relref "5.5.5-Reporting">}})