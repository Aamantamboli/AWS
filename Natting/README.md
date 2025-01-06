# Natting in AWS

This guide will walk you through the process of configuring NATting in AWS to provide internet access to instances in a private subnet while keeping them isolated from direct inbound internet traffic.

## Prerequisites

- AWS Account
- Basic knowledge of AWS services (VPC, Subnet, EC2)
- A working VPC configuration

---

## Step 1: Create a VPC

1. **Login** to the AWS Management Console and navigate to the **VPC Dashboard**.
2. Create a new **VPC**. This will serve as the network environment for your instances.

 ![image](https://github.com/user-attachments/assets/462e215e-48d3-4491-946a-53c23e728aa6)

---

## Step 2: Create Two Subnets (Public and Private)

1. Create two subnets:
   - A **public subnet** for the instances that will have direct access to the internet.
   - A **private subnet** for the instances that will not have direct access to the internet but can access the internet through NAT.

   **Public Subnet**:<br>
  ![image](https://github.com/user-attachments/assets/2aa555d6-a05a-4be2-a7fe-6f803855a5d9)

   **Private Subnet**:<br>
  ![image](https://github.com/user-attachments/assets/1994c370-1ef4-4195-899e-ff21c6f942b6)

   **Subnet Configuration**:
   - Ensure each subnet is associated with the correct route table (public or private).

---

## Step 3: Create an Internet Gateway and Attach It to the VPC

1. Go to the **Internet Gateways** section in the VPC dashboard.
2. Create a new **Internet Gateway** and attach it to the VPC.

![image](https://github.com/user-attachments/assets/bbe340a9-ccbb-4288-a9c9-609bd82c1d3b)

---

## Step 4: Create a NAT Gateway and Allocate Elastic IP

1. Navigate to the **NAT Gateways** section and create a new **NAT Gateway**.
2. Select the **public subnet** and allocate an **Elastic IP** for the NAT Gateway.

![image](https://github.com/user-attachments/assets/21129122-6c96-425c-a82f-4b15ec71f164)

---

## Step 5: Create a Route Table for the Public Subnet

1. Go to the **Route Tables** section in your VPC dashboard.
2. Create a new **route table** for the **public subnet**.
   
![image](https://github.com/user-attachments/assets/06257200-3f6c-4c3b-8ba5-545ed1b95175)

---

## Step 6: Edit the Route Table and Add the Internet Gateway

1. Edit the route table for the public subnet.
2. Add a route that directs all outbound traffic (0.0.0.0/0) to the **Internet Gateway**.

![image](https://github.com/user-attachments/assets/ec1ca5f5-2669-448f-ba19-9912b9aa1632)

---

## Step 7: Edit Subnet Associations and Select the Public Subnet

1. Associate the **public subnet** with the newly created route table to ensure proper routing of internet-bound traffic.

![image](https://github.com/user-attachments/assets/bae85b75-490c-44e1-8c3f-b19dd063490e)

---

## Step 8: Create a Route Table for the Private Subnet

1. Create a new **route table** for the **private subnet**.

![image](https://github.com/user-attachments/assets/66e93428-67da-43d0-90a7-ebdc71b849ad)

---

## Step 9: Edit the Route Table and Add the NAT Gateway

1. Edit the route table for the private subnet.
2. Add a route that directs outbound traffic (0.0.0.0/0) to the **NAT Gateway**.

![image](https://github.com/user-attachments/assets/3476e87d-a05e-457e-b6b3-7806fef6a85c)

---

## Step 10: Edit Subnet Associations and Select the Private Subnet

1. Associate the **private subnet** with the newly created route table to enable NAT-based internet access.

![image](https://github.com/user-attachments/assets/237c57a9-abd8-4298-adb5-4bd412de61ff)

---

## Step 11: Launch a Public EC2 Instance

1. Launch a new **public EC2 instance**.
2. In the **network settings**, select the **VPC** you created and choose the **public subnet**.
3. Enable **auto-assign public IP** to make the instance publicly accessible.

![image](https://github.com/user-attachments/assets/1ad2c7d4-babd-4994-9e49-b3dea1efa248)

---

## Step 12: Launch a Private EC2 Instance

1. Launch a new **private EC2 instance**.
2. In the **network settings**, select the **VPC** you created and choose the **private subnet**.
3. Disable **auto-assign public IP** as this instance will not have direct internet access.

 ![image](https://github.com/user-attachments/assets/cf56f0b6-aa45-4818-bfc7-6618867a9f8d)

---

## Step 13: Connect to the Public EC2 Instance

1. Copy the **public IP** of your public EC2 instance.
2. Open **MobaXterm** (or your preferred SSH client) and paste the **public IP**.
3. Select your **key pair** to connect via SSH.

![image](https://github.com/user-attachments/assets/13af8a4c-cf1e-4b8c-998f-e7d22e1fb531)

---

## Step 14: Upload Your Key

1. Make sure the **key file** is available for use when connecting to the instance.

![image](https://github.com/user-attachments/assets/353331a0-19ad-4b15-b926-5cdcb870735b)

---

## Step 15: Change Permission of the Private Key File

1. Change the permission of the key file to `400` for security reasons.

![image](https://github.com/user-attachments/assets/25145b5a-8210-442c-b4c0-8af7b11fad7d)

---

## Step 16: Connect to the Private Instance

1. Once connected to the public instance, use SSH to connect to the private instance by pasting the **private IP** of the private EC2 instance.
   
![image](https://github.com/user-attachments/assets/c4a99f81-9287-4dfb-a9ce-a3741be841b7)

---

## Security Group Settings

- Ensure that the following ports are open in the **Security Group** for both instances:
  - **SSH (port 22)**
  - **HTTP (port 80)**
  - **HTTPS (port 443)**
  - **TCP (port 3000 or any other required ports)**

---

## Conclusion

You have successfully configured NATting in AWS to provide internet access to your private subnet while maintaining security. The public subnet can access the internet directly, and the private subnet can access the internet through the NAT Gateway.

---

### References
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/)
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
```
