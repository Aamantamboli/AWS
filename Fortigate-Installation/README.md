# FortiGate Installation on AWS EC2

This guide will walk you through the steps of launching a FortiGate instance on AWS EC2, configuring it, and accessing it via the browser.

## Prerequisites

- An AWS account
- Basic understanding of AWS EC2, Security Groups, and AMI (Amazon Machine Image)

---

## Step 1: Create an EC2 Instance

1. **Login to your AWS Management Console** and navigate to the EC2 dashboard.
2. Click on **Launch Instance** to create a new EC2 instance.
   
![image](https://github.com/user-attachments/assets/dc795962-d9a1-4ba5-84e5-d4e43d683db2)

3. Choose the appropriate configuration (instance type, VPC, subnet, etc.) for your needs.

---

## Step 2: Search for the FortiGate AMI

1. In the **AWS EC2 Dashboard**, under **Launch Instance**, go to the **Marketplace** tab.
2. Search for **FortiGate** in the search bar to find the available FortiGate AMI.

![image](https://github.com/user-attachments/assets/c6dfd91d-e7e5-44a7-b6f2-82e834365181)

---

## Step 3: Select and Subscribe to the FortiGate AMI

1. Select the appropriate **FortiGate AMI** for your version (e.g., FortiGate 7.0.0).
2. Click **Select** to start the instance configuration.
3. You will be asked to **Subscribe** to the FortiGate AMI if you haven't already. Follow the on-screen prompts to subscribe.

![image](https://github.com/user-attachments/assets/afe6617b-887c-46dd-95a5-95473d0378d7)

---

## Step 4: Launch the Instance and Access it via Browser

1. Follow the standard EC2 instance launch process (select instance type, configure instance details, add storage, configure security group).
2. Ensure that you open **TCP Port 3000** in your security group to allow access to FortiGate’s web interface.
3. Once the instance is launched, you will see the **Public IP** of your instance. Copy this IP address.
4. Open a browser and enter the following URL, replacing `your-public-ip` with the actual public IP address of the instance:
   
   ```
   https://your-public-ip:3000
   ```

![image](https://github.com/user-attachments/assets/41088b59-fdf2-4142-aedc-f7f5ee2492cd)

---

## Step 5: Login to FortiGate Web Interface

1. When prompted, enter the **username** as `admin` and the **password** as your **instance ID** (this is the default password).

![image](https://github.com/user-attachments/assets/906ae900-7f9a-42e0-98b1-902dc9e806fe)

2. After logging in, you will be asked to **reset the password** for security purposes. Choose a strong password for your FortiGate instance.

---

## Step 6: Successfully Launched FortiGate

1. Once the password is reset, you will have full access to the FortiGate web interface.

![image](https://github.com/user-attachments/assets/07c0c01c-f51c-4071-860d-9625c2690afd)

---

## Important Notes

- **Security Group**: Ensure that **TCP port 3000** is open in the security group of your EC2 instance. This is essential to access the FortiGate web interface.
- **Username**: The default username is `admin`.
- **Password**: The default password is the **Instance ID** at the time of launch. Make sure to reset the password once you log in.

---

## Conclusion

You have successfully launched and accessed a **FortiGate** instance on AWS EC2. From here, you can configure the firewall rules, VPN, or any other FortiGate features as per your requirements.

For more information, refer to the [FortiGate Documentation](https://fortinetweb.com) for advanced configuration options.

---

### References
- [AWS EC2 Documentation](https://aws.amazon.com/ec2/)
- [FortiGate Documentation](https://docs.fortinet.com/)
