---

title : "Create Route Table"

date : "`r Sys.Date()`"

weight : 4

chapter : false

pre : " <b> 5.1.4 </b> "

---

### Steps

1. Go to **VPC → Route Tables** and select **Create route table**.

   ![Route Table](/images/01/image_017.png)

2. Enter the name of the Route Table and select the project VPC:

   **Name:** `Automation-Public-RT`

   **VPC:** `Automation-VPC`

   Then select **Create route table**.

   ![Route Table](/images/01/image_018.png)

3. This is the interface of **Automation-Public-RT** after it has been successfully created.

   ![Route Table](/images/01/image_019.png)

4. Next, we will configure the Internet route for the Public Route Table.

   Select the **Routes** tab and then select **Edit routes**.

   ![Route Table](/images/01/image_020.png)

5. In the **Edit routes** interface, select **Add route**.

6. Configure the route:

   * **Destination:**

     `0.0.0.0/0`

   * **Target:** select **Internet Gateway** and choose:

     `Automation-IGW`

   The `0.0.0.0/0` route means that packets destined for networks that do not match any other specific routes will be sent to the Internet Gateway.

   Then select **Save changes**.

   ![Route Table](/images/01/image_021.png)

7. Next, we will associate the Route Table with the **Public Subnet**.

   In **Automation-Public-RT**, switch to the **Subnet associations** tab and select **Edit subnet associations**.

   ![Route Table](/images/01/image_022.png)

8. Select:

   `Automation-Public-Subnet`

   Then select **Save associations**.

   ![Route Table](/images/01/image_023.png)

9. After the association is successfully completed, **Automation-Public-RT** will be associated with **Automation-Public-Subnet**.

   ![Route Table](/images/01/image_024.png)

10. Next, create a Route Table for the Private Subnet.

    Enter the name:

    `Automation-Private-RT`

    Select the VPC:

    `Automation-VPC`

    Then associate this Route Table with:

    `Automation-Private-Subnet`

    ![Route Table](/images/01/image_025.png)

After completing the configuration, the system has two Route Tables:

| Route Table | Subnet Association | Purpose |
| ----------------------- | --------------------------- | ------------------------------ |
| `Automation-Public-RT` | `Automation-Public-Subnet` | Routing for Automation Server |
| `Automation-Private-RT` | `Automation-Private-Subnet` | Routing for Managed Nodes |

