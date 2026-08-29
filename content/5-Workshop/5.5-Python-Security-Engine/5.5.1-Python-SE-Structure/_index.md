---

title : "Python Security Engine"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.5.1 </b> "

---

### Overview

In this project, the **Python Security Engine** is responsible for processing and analyzing security information after Ansible performs tasks on the Managed Nodes.

Unlike Ansible, which focuses on automation and configuration management, the Python component focuses on security checking logic, Security Finding processing, state management, reporting, and remediation support.

All Python components are organized under:

~~~text
python/
~~~

### Python Structure

The main structure of the Python Security Engine is:

~~~text
python/

├── main.py
│
├── checks/
│   ├── firewall_checks.py
│   └── ssh_checks.py
│
├── models/
│   └── finding.py
│
├── security_engine/
│   ├── ansible_runner.py
│   ├── engine.py
│   ├── policy_loader.py
│   └── remediation.py
│
└── reporters/
    ├── console.py
    └── json_reporter.py
~~~

![ASAU](/images/01/image_234.png)

### Components

1. **`main.py`**

   - Entry point of the Python application.
   - Coordinates the components of the Security Engine.

2. **`checks/`**

   - Contains modules responsible for security checks.
   - `ssh_checks.py`: performs SSH-related checks.
   - `firewall_checks.py`: performs Firewall-related checks.

3. **`models/`**

   - Contains data models used by the application.
   - `finding.py` defines the structure of a Security Finding.

4. **`security_engine/`**

   - Contains the core Security Engine logic.
   - `ansible_runner.py`: interacts with Ansible.
   - `engine.py`: handles the main Security Engine logic.
   - `policy_loader.py`: loads the Security Policy.
   - `remediation.py`: handles the remediation process.

5. **`reporters/`**

   - Contains components responsible for generating output.
   - `console.py`: displays results in the console.
   - `json_reporter.py`: exports results in JSON format.

### Overall Workflow

The Python components work together through the following workflow:

~~~text
                    main.py

                       ↓

                Security Engine

                       |

         +-------------+-------------+
         |             |             |
         ↓             ↓             ↓

      Checks       Policies       Ansible

         |             |             |

         +-------------+-------------+

                       ↓

                    Finding

                       ↓

                   Reporting

                  /          \

                 ↓            ↓

              Console        JSON
~~~

The Security Engine receives information from the related components, performs checks according to the defined policies, generates Security Findings, and sends the results to the reporting components.

### Relationship Between Ansible and Python

In the project architecture, Ansible and Python have different responsibilities:

~~~text
              Automation Server

                      |

          +-----------+-----------+
          |                       |
          ↓                       ↓

       Ansible                  Python

          |                       |

          ↓                       ↓

 Configuration            Security Analysis
   & Automation                   |
          |                       ↓
          |                    Finding
          |                       |
          +-----------+-----------+
                      |
                      ↓
                    Output
~~~

Ansible focuses on **automation and configuration management**, while Python focuses on **security checking, Finding processing, remediation, and reporting**.

### Main Functional Groups

The Python Security Engine is divided into the following functional groups:

~~~text
Python Security Engine

│
├── Checks
│   ├── SSH
│   └── Firewall
│
├── Security Engine
│   ├── Ansible Runner
│   ├── Policy Loader
│   └── Remediation
│
├── Models
│   └── Finding
│
└── Reporters
    ├── Console
    └── JSON
~~~

This structure separates **checking**, **processing**, **data modeling**, and **reporting** into independent components.

### Result

After building the Python Security Engine, the project has a dedicated component for processing security information alongside Ansible:

~~~text
Ansible

   ↓

Automation / Configuration

   ↓

Managed Nodes

   ↓

Python Security Engine

   ↓

Security Checks

   ↓

Finding

   ↓

Reports / Remediation
~~~

The next section will focus on **Security Checks**, particularly how `ssh_checks.py` and `firewall_checks.py` verify the security status of the Managed Nodes.