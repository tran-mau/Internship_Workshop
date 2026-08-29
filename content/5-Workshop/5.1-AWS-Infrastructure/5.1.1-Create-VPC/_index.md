---

title : "Create VPC"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.1.1 </b> "

---

### Steps

1. Go to the **AWS Console**, enter **VPC** in the search bar, and then select the **VPC** service.

   ![VPC](/images/01/image_001.png)

2. After accessing the VPC service, select **Your VPCs** and then select **Create VPC**.

   ![VPC](/images/01/image_002.png)

3. After selecting **Create VPC**, we will see the interface for entering the VPC information:

   * In **Resources to create**, select **VPC only** because in this project we want to configure the network components such as Subnet, Internet Gateway, and Route Table manually.

   * In **Name tag – optional**, enter **Automation-VPC**. This name is used to identify the VPC in the project.

   * In **IPv4 CIDR block**, select **IPv4 CIDR manual input** to manually define the IPv4 address range for the VPC.

   * In **IPv4 CIDR**, enter:

     ```text
     10.0.0.0/16
     ```

     This address range is used as the network address space for the entire project infrastructure.

   * In **IPv6 CIDR block**, select **No IPv6 CIDR block** because the project does not use IPv6.

   * In **Tenancy**, select **Default**. With this configuration, EC2 instances will use AWS shared physical hardware instead of requiring dedicated hardware.

   * After completing the information, select **Create VPC** to create the VPC.

   ![VPC](/images/01/image_003.png)

4. After successfully creating the VPC, **Automation-VPC** will appear in the VPC list.

   This VPC will serve as the foundation for deploying the remaining components of the system, including:

   * **Automation-Public-Subnet**

   * **Automation-Private-Subnet**

   * **Automation-IGW**

   * **Automation-Public-RT**

   * **Automation-Private-RT**

   * The EC2 instances of the project

   ![VPC](/images/01/image_004.png)