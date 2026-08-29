---

title : "Set Up SSH Connection to Managed Nodes"

date : "`r Sys.Date()`"

weight : 5

chapter : false

pre : " <b> 5.2.5 </b> "

---

### Steps

After completing the AWS infrastructure, the Automation Server needs to be able to establish SSH connections to `Managed-Node-01` and `Managed-Node-02`.

In the project, SSH is used as the connection method between the **Automation Server** and **Managed Nodes** so that Ansible can manage these servers.

## 1. Check Network Connectivity

Before configuring SSH authentication, we need to check connectivity to the Managed Nodes and the SSH port.

The Managed Nodes are located in the Private Subnet, and the `Managed-Node-SG` Security Group allows TCP port 22 from `Automation-SG`.

![ATSV](/images/01/image_086.png)

## 2. Create an SSH Key for the Automation Server

On the **Automation Server**, create a dedicated SSH key:

```bash
ssh-keygen -t ed25519 -C "automation-ansible"
```

The command above creates an SSH key pair using the **Ed25519** algorithm.

After creation, the Automation Server will have:

```text
~/.ssh/id_ed25519

~/.ssh/id_ed25519.pub
```

Where:

- `id_ed25519` is the **private key**.
- `id_ed25519.pub` is the **public key**.

The private key is kept on the Automation Server and is not copied to the Managed Nodes.

![ATSV](/images/01/image_081.png)

## 3. Add the Public Key to the Managed Nodes

The goal is to add:

```text
~/.ssh/id_ed25519.pub
```

to the following file on the Managed Nodes:

```text
~/.ssh/authorized_keys
```

Authentication mechanism:

```text
Automation Server

       |

       | Private Key

       ↓

Managed Node

       |

       | Public Key

       ↓

~/.ssh/authorized_keys
```

The Managed Node stores the public key in `authorized_keys`, while the Automation Server keeps the private key.

## 4. Use SSH Agent Forwarding

First, check the SSH Agent on the Windows machine.

Then SSH into the Automation Server with **Agent Forwarding** enabled.

After logging in to the Automation Server, check:

```bash
ssh-add -l
```

If the key fingerprint is displayed, the Automation Server can use the key through the SSH Agent while the actual private key remains on the Windows machine.

## 5. Connect to the Managed Node

From the Automation Server, SSH to the Managed Node.

For example:

```bash
ssh ubuntu@10.0.2.171
```

After logging in to the Managed Node, create the SSH directory:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

Then open the file:

```bash
nano ~/.ssh/authorized_keys
```

Add the Automation Server's public key to the `authorized_keys` file and set the appropriate permissions:

```bash
chmod 600 ~/.ssh/authorized_keys
```

![ATSV](/images/01/image_091.png)

![ATSV](/images/01/image_092.png)

![ATSV](/images/01/image_093.png)

These steps allow the Managed Node to authenticate the Automation Server using the public key.

![ATSV](/images/01/image_086.png)

![ATSV](/images/01/image_087.png)

## 6. Test SSH Using the SSH Key

After configuring the public key, test the connection from the Automation Server:

```bash
ssh -i ~/.ssh/id_ed25519 ubuntu@10.0.2.171
```

If the connection is successful, the Automation Server can SSH to the Managed Node using the SSH key.

![ATSV](/images/01/image_089.png)

Perform the same configuration for `Managed-Node-02`.

## 7. Create SSH Config

To avoid entering the full IP address and SSH key every time, create the following file:

```bash
nano ~/.ssh/config
```

Configuration:

```text
Host managed-01

    HostName 10.0.2.171

    User ubuntu

    IdentityFile ~/.ssh/id_ed25519

Host managed-02

    HostName 10.0.2.102

    User ubuntu

    IdentityFile ~/.ssh/id_ed25519
```

![ATSV](/images/01/image_095.png)

Where:

- `managed-01` and `managed-02` are the hostnames used for connecting to the Managed Nodes.
- `HostName` is the private IP address of the Managed Node.
- `User` is the `ubuntu` user.
- `IdentityFile` specifies the SSH private key to be used.

This configuration is used in the project to simplify connections to the two Managed Nodes.

Then set the appropriate permissions:

```bash
chmod 600 ~/.ssh/config
```

![ATSV](/images/01/image_096.png)

## 8. Test the Connection Using Hostnames

After creating the SSH Config, connections can be established directly using:

```bash
ssh managed-01
```

and:

```bash
ssh managed-02
```

If both connections are successful, SSH communication between the Automation Server and Managed Nodes has been successfully configured.

```text
Automation Server

       |

       +── ssh managed-01

       |

       └── ssh managed-02
```

![ATSV](/images/01/image_097.png)

![ATSV](/images/01/image_098.png)

## Result

After completing the configuration, the system has the following connection model:

```text
                     Automation Server

                            |

                     SSH Authentication

                            |

              +-------------+-------------+

              |                           |

         managed-01                  managed-02

              |                           |

      Managed-Node-01             Managed-Node-02

        Private EC2                  Private EC2
```

The Automation Server can now establish SSH connections to both Managed Nodes using SSH keys. This provides the foundation for configuring the **Ansible Inventory** and allowing Ansible to manage the Managed Nodes.