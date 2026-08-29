---

title : "Security Audit"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.4.3 </b> "

---

### Overview

After deploying **SSH Hardening** and **Firewall**, the project needs a mechanism to verify the security status of the Managed Nodes.

In the Ansible section, the **Security Audit** functionality is organized through:

~~~text
ansible/playbooks/security_audit.yml
~~~

This Playbook is used to perform security checks on the Managed Nodes.

### 1. `security_audit.yml` Playbook

File:

~~~text
ansible/playbooks/security_audit.yml
~~~

acts as the orchestrator for the Security Audit process.

The general workflow is:

~~~text
Automation Server

        |

      Ansible

        |

security_audit.yml

        ↓

Managed Nodes

        ↓

Security Audit
~~~

![ASAU](/images/01/image_231.png)

### 2. Purpose of Security Audit

Security Audit is used to verify the security configuration status of the Managed Nodes.

In this project, the audit focuses on the security components that have already been deployed, particularly:

~~~text
Managed Node

    |

    +── SSH configuration

    |

    └── Firewall configuration
~~~

The audit results are used to determine the security status of each Managed Node.

### 3. How Security Audit Works

When the Playbook is executed, Ansible uses the Inventory to determine which Managed Nodes need to be checked.

The tasks defined in `security_audit.yml` are then executed on the target hosts.

~~~text
Inventory

    |

    ↓

security_audit.yml

    |

    ↓

Audit Tasks

    |

    ↓

Managed-Node-01

Managed-Node-02
~~~

The tasks collect or verify information related to the security status of the Managed Nodes.

### 4. Relationship with Security Components

Security Audit is performed after the security configurations have been deployed.

~~~text
             Security

                 |

       +---------+---------+
       |                   |
       ↓                   ↓

 SSH Hardening         Firewall

       |                   |

       +---------+---------+

                 |

                 ↓

          Security Audit

                 |

                 ↓

           Audit Result
~~~

The roles of each component are:

- **SSH Hardening** applies security configurations to the SSH service.
- **Firewall** controls network traffic on the Managed Nodes.
- **Security Audit** verifies the resulting security configuration.

### 5. Execute Security Audit

From the Automation Server, run:

~~~bash
ansible-playbook -i ansible/inventory/hosts.ini ansible/playbooks/security_audit.yml
~~~

Where:

- `ansible-playbook`: Executes the Ansible Playbook.
- `-i`: Specifies the Inventory.
- `hosts.ini`: Defines the Managed Nodes.
- `security_audit.yml`: Specifies the Playbook used for Security Audit.

![ASAU](/images/01/image_232.png)

### 6. Verify the Results

After the Playbook finishes, check the output to confirm that the Security Audit was executed successfully.

~~~text
Security Audit

      |

      +── Managed-Node-01

      |

      └── Managed-Node-02
~~~

![ASAU](/images/01/image_233.png)

The Audit results can then be used by the **Python Security Engine** for further security analysis.

### 7. Overall Workflow

The overall Security Audit workflow is:

~~~text
                  Automation Server

                         |

                       Ansible

                         |

                      Inventory

                         |

                         ↓

                security_audit.yml

                         |

               +---------+---------+
               |                   |
               ↓                   ↓

        Managed-Node-01     Managed-Node-02

               |                   |

               +---------+---------+

                         |

                         ↓

                   Security Audit

                         |

                         ↓

                     Audit Result
~~~

Security Audit represents the transition from **security configuration** to **security status verification**.

### Result

After completing this section, the project follows the workflow:

~~~text
Configure

    ↓

SSH Hardening + Firewall

    ↓

Security Audit

    ↓

Check Security Status
~~~

Ansible is responsible for performing the security checks on the Managed Nodes. The resulting data provides the foundation for the **Python Security Engine**, which will perform further analysis and processing.