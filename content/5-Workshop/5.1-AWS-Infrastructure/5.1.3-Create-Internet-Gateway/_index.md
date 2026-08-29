---

title : "Create Internet Gateway"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.1.3 </b> "

---

### Steps

1. In the **VPC** interface, select **Internet Gateways** and then select **Create internet gateway**.

   ![Internet Gateway](/images/01/image_011.png)

2. In the Internet Gateway creation interface, enter the name:

   `Automation-IGW`

   Then select **Create internet gateway**.

   ![Internet Gateway](/images/01/image_012.png)

3. After successfully creating it, we will see **Automation-IGW** in the list of Internet Gateways.

   ![Internet Gateway](/images/01/image_013.png)

   Initially, the **State** of the Internet Gateway is **Detached**. This means that the Internet Gateway is not attached to the `Automation-VPC`.

   To use the Internet Gateway, we need to attach it to the VPC.

4. Select **Actions** → **Attach to a VPC**.

   ![Internet Gateway](/images/01/image_014.png)

5. In the VPC selection section, select:

   `Automation-VPC`

   Then select **Attach internet gateway**.

   ![Internet Gateway](/images/01/image_015.png)

6. After successfully attaching it, the **State** of the Internet Gateway will change to **Attached**.

   This indicates that `Automation-IGW` has been attached to `Automation-VPC` and is ready to be used in the routing configuration of the Public Subnet.