---

title : "Security Engine"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.5.3 </b> "

---

### Overview

The **Security Engine** is the central component of the Python Security Engine. It coordinates the security checking process and connects components such as Security Checks, Security Policy, Ansible, and Finding.

The main files related to the Security Engine are:

~~~text
python/security_engine/

├── ansible_runner.py
├── engine.py
├── policy_loader.py
└── remediation.py
~~~

Their responsibilities are:

- `engine.py`: handles the core Security Engine logic.
- `ansible_runner.py`: connects Python with Ansible and executes automation tasks.
- `policy_loader.py`: loads the Security Policy.
- `remediation.py`: handles the security remediation process.

![ASAU](/images/01/image_239.png)

### 1. Role of the Security Engine

The Security Engine connects the different stages of the security workflow:

~~~text
Security Policy

       ↓

Security Engine

       |

   +---+---+
   |       |
   ↓       ↓

 Checks   Ansible

   |       |

   +---+---+

       ↓

    Finding

       ↓

 Remediation
~~~

This centralized approach prevents the security workflow from being scattered across individual modules.

### 2. `engine.py`

File:

~~~text
python/security_engine/engine.py
~~~

is the central component of the Security Engine.

It coordinates the processing between security checks, policies, findings, and remediation.

![ASAU](/images/01/image_240.png)

![ASAU](/images/01/image_241.png)

The general workflow is:

~~~text
Input
 |
 ↓
engine.py
 |
 +── Load Policy
 |
 +── Run Checks
 |
 +── Process Findings
 |
 └── Remediation
~~~

### 3. `ansible_runner.py`

File:

~~~text
python/security_engine/ansible_runner.py
~~~

connects the Python Security Engine with Ansible.

The relationship between the two components is:

~~~text
Python Security Engine

          ↓

   ansible_runner.py

          ↓

        Ansible

          ↓

    Managed Nodes
~~~

This allows Python to use Ansible as the automation layer for executing configuration changes on the Managed Nodes.

![ASAU](/images/01/image_242.png)

![ASAU](/images/01/image_243.png)

### 4. `policy_loader.py`

File:

~~~text
python/security_engine/policy_loader.py
~~~

is responsible for loading the Security Policy.

The project's Security Policy is stored in:

~~~text
ansible/policies/security_policy.yml
~~~

The processing flow is:

~~~text
security_policy.yml

        ↓

policy_loader.py

        ↓

Security Engine

        ↓

Security Checks
~~~

Separating the Policy from the application logic allows security requirements to be managed independently from the Security Engine implementation.

![ASAU](/images/01/image_244.png)

### 5. `remediation.py`

File:

~~~text
python/security_engine/remediation.py
~~~

is responsible for the **Remediation** process.

After the system detects a security issue, remediation is performed to bring the Managed Node back to the desired security state.

The general workflow is:

~~~text
Security Check

      ↓

   Finding

      ↓

 Remediation

      ↓

 Managed Node
~~~

![ASAU](/images/01/image_245.png)

![ASAU](/images/01/image_246.png)

![ASAU](/images/01/image_247.png)

### 6. Relationship Between the Components

The files under `security_engine/` work together as follows:

~~~text
                 engine.py

                    |

       +------------+------------+
       |            |            |
       ↓            ↓            ↓

policy_loader  ansible_runner  remediation

       |            |            |

       ↓            ↓            ↓

 Security       Ansible       Fix
 Policy            |            |
                   ↓            |
             Managed Nodes <----+
~~~

Their responsibilities can be summarized as:

- `policy_loader.py` provides the Security Policy.
- `ansible_runner.py` connects the Security Engine with Ansible.
- `engine.py` coordinates the overall process.
- `remediation.py` handles security remediation.

### 7. Overall Workflow

The Security Engine is positioned at the center of the security workflow:

~~~text
                    Security Policy

                          ↓

                    policy_loader.py

                          ↓

                       engine.py

                          |

              +-----------+-----------+
              |                       |
              ↓                       ↓

       Security Checks        ansible_runner.py

              |                       |

              ↓                       ↓

           Finding                 Ansible

              |                       |

              +-----------+-----------+

                          ↓

                    remediation.py

                          ↓

                    Managed Nodes
~~~

The overall security process can be summarized as:

~~~text
Policy

  ↓

Check

  ↓

Finding

  ↓

Remediation
~~~

### 8. Result

After implementing the Security Engine, the project has a central component that connects:

~~~text
Security Policy

      ↓

Security Checks

      ↓

Security Engine

      ↓

Ansible

      ↓

Managed Nodes

      ↓

Finding / Remediation
~~~

The Security Engine acts as a bridge between **Python-based security analysis logic** and **Ansible-based automation capabilities**.