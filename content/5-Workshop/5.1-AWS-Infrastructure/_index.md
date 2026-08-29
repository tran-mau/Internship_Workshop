---

title : "AWS Infrastructure"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.1 </b> "

---

### Overview

In this section, we build the AWS infrastructure as the foundation for the Enterprise Infrastructure Automation system.

The environment is deployed in the AWS Region **Asia Pacific (Singapore) – `ap-southeast-1`**, using a dedicated VPC with two Subnets:

* **Public Subnet**: used for the Automation Server.

* **Private Subnet**: used for Managed-Node-01 and Managed-Node-02.

The general network architecture:

~~~text
                        AWS VPC

                      10.0.0.0/16

                           |

              +-------------+-------------+

              |                           |

       Public Subnet               Private Subnet

        10.0.1.0/24                10.0.2.0/24

              |                           |

       Automation Server          +--------+--------+

                                  |                 |

                            Managed-Node-01   Managed-Node-02
~~~

<!--
Insert image: AWS Infrastructure architecture diagram of the project.
-->

### List of Practical Chapters

+ [5.1.1 Create VPC]({{< relref "5.1.1-Create-VPC">}})

+ [5.1.2 Create Subnet]({{< relref "5.1.2-Create-Subnet">}})

+ [5.1.3 Create Internet Gateway]({{< relref "5.1.3-Create-Internet-Gateway">}})

+ [5.1.4 Create Route Table]({{< relref "5.1.4-Create-Route-Table">}})

+ [5.1.5 Security Group]({{< relref "5.1.5-Security-Group">}})

+ [5.1.6 Deploy EC2]({{< relref "5.1.6-Deploy-EC2">}})

+ [5.1.7 IAM Role]({{< relref "5.1.7-IAM-Role">}})

+ [5.1.8 Setup SSH]({{< relref "5.1.8-Setup-SSH">}})