---

title : "Create Subnet"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.1.2 </b> "

---

### Steps

1. Go to the **AWS Console**, search for **Subnet**, and select **VPC → Subnets**.

   ![Subnet](/images/01/image_005.png)

2. After accessing the Subnets interface, select **Create subnet**.

   ![Subnet](/images/01/image_001.png)

   * First, select the VPC that we created in the previous step:

     `Automation-VPC`

   ![Subnet](/images/01/image_007.png)

   * Next, enter the information in **Subnet settings**:

     * **Subnet name:** `Automation-Public-Subnet`

     * **Availability Zone:** select `ap-southeast-1a`

     * **IPv4 VPC CIDR block:** `10.0.0.0/16`

     * **IPv4 subnet CIDR block:** `10.0.1.0/24`

     The `10.0.1.0/24` range is used for the Public Subnet, where the **Automation Server** will be deployed.

   ![Subnet](/images/01/image_008.png)

3. After successfully creating the subnet, **Automation-Public-Subnet** will appear in the list of Subnets of `Automation-VPC`.

   ![Subnet](/images/01/image_009.png)

4. Continue creating a Private Subnet for the Managed Nodes.

   Select **Create subnet** and use the VPC:

   `Automation-VPC`

   Then configure:

   * **Subnet name:** `Automation-Private-Subnet`

   * **Availability Zone:** `ap-southeast-1a`

   * **IPv4 VPC CIDR block:** `10.0.0.0/16`

   * **IPv4 subnet CIDR block:** `10.0.2.0/24`

   This Private Subnet will be used to deploy:

   * `Managed-Node-01`

   * `Managed-Node-02`

   ![Subnet](/images/01/image_010.png)

5. After completing the configuration, we have two Subnets in `Automation-VPC`:

   | Subnet | CIDR | Purpose |
   | --------------------------- | ------------- | ----------------------------------- |
   | `Automation-Public-Subnet` | `10.0.1.0/24` | Automation Server |
   | `Automation-Private-Subnet` | `10.0.2.0/24` | Managed-Node-01 and Managed-Node-02 |

These two Subnets will be used in the following steps to build the Public/Private architecture for the automation system.