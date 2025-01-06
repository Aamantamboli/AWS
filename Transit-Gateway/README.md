# Transit Gateway Setup in AWS (Same Region)

This guide outlines the steps to create and configure a Transit Gateway within the same region, connecting three different Virtual Private Clouds (VPCs) and enabling communication between instances hosted in these VPCs.

---

## Prerequisites

- AWS account with sufficient permissions
- Basic knowledge of AWS VPC, subnets, internet gateways, and route tables
- MobaXterm or any SSH client to connect to EC2 instances

---

## Step-by-Step Guide

### Step 1: Create 1st VPC (Virtual Private Cloud)
Create the first VPC, which will be connected to the other two VPCs via the Transit Gateway.

![image](https://github.com/user-attachments/assets/bc9083b5-d4fb-4530-978c-7ca8f418ee83)

### Step 2: Create a Subnet for the 1st VPC
Create a subnet within the 1st VPC to host instances.

![image](https://github.com/user-attachments/assets/906134e7-3be7-4ea0-8ba8-d96b16878c61)

### Step 3: Create 1st Internet Gateway
Create an internet gateway for the 1st VPC to provide internet access.

![image](https://github.com/user-attachments/assets/96c0995b-9f8a-4b98-9a40-1dc5460fe76e)

### Step 4: Attach the 1st Internet Gateway to the 1st VPC
Attach the created internet gateway to the 1st VPC.

![image](https://github.com/user-attachments/assets/5affd5c5-4f8a-4cc3-862a-5f60cbf615f4)

### Step 5: Create 2nd VPC (Virtual Private Cloud)
Create the second VPC in the same region.

![image](https://github.com/user-attachments/assets/b48bdf42-0bfb-4e08-b13b-12c329956bd8)

### Step 6: Create a Subnet for the 2nd VPC
Create a subnet within the 2nd VPC for hosting instances.

![image](https://github.com/user-attachments/assets/54903ed8-ab66-4475-b426-fa2418ada0ce)

### Step 7: Create 2nd Internet Gateway
Create an internet gateway for the 2nd VPC.

![image](https://github.com/user-attachments/assets/85106f9b-2df6-47ee-83a7-3292f387dbce)

### Step 8: Attach the 2nd Internet Gateway to the 2nd VPC
Attach the created internet gateway to the 2nd VPC.

![image](https://github.com/user-attachments/assets/2d5dea52-e6c4-4698-9a5f-feb99443baf1)

### Step 9: Create 3rd VPC (Virtual Private Cloud)
Create the third VPC for the setup.

![image](https://github.com/user-attachments/assets/acaab63b-993f-4d9d-8d0b-68da157dd1d6)

### Step 10: Create a Subnet for the 3rd VPC
Create a subnet within the 3rd VPC for instances.

![image](https://github.com/user-attachments/assets/204fce89-1943-49ec-b979-0e7687c40d96)

### Step 11: Create 3rd Internet Gateway
Create an internet gateway for the 3rd VPC.

![image](https://github.com/user-attachments/assets/2c100e7e-3465-4c92-8800-b87316bb054e)

### Step 12: Attach the 3rd Internet Gateway to the 3rd VPC
Attach the created internet gateway to the 3rd VPC.

![image](https://github.com/user-attachments/assets/d1418d95-c6a1-4410-a33c-0e392503fa34)

### Step 13: Create a Transit Gateway
Create a Transit Gateway to connect the three VPCs.

![image](https://github.com/user-attachments/assets/00b6161d-fd4c-468e-8634-44e433ce3d03)

### Step 14: Create Transit Gateway Attachment for the 1st VPC
Attach the 1st VPC to the Transit Gateway.

![image](https://github.com/user-attachments/assets/c944294b-56a6-4142-bc90-9bc7bef2e6e8)

### Step 15: Create Transit Gateway Attachment for the 2nd VPC
Attach the 2nd VPC to the Transit Gateway.

![image](https://github.com/user-attachments/assets/f31cebaf-fcff-431a-8f35-e89fb92b76a0)

### Step 16: Create Transit Gateway Attachment for the 3rd VPC
Attach the 3rd VPC to the Transit Gateway.

![image](https://github.com/user-attachments/assets/557f1ee0-45cc-4868-a554-f922f9be4394)

### Step 17: Create Route Table for the 1st VPC
Create the route table for the 1st VPC to enable routing.

![image](https://github.com/user-attachments/assets/a74b00cc-5833-4229-98e9-011dd6a585ef)

### Step 18: Edit 1st Route Table - Add Internet Gateway and Transit Gateway
Edit the 1st route table to add the internet gateway and the Transit Gateway, and provide the CIDR of the other VPCs.

![image](https://github.com/user-attachments/assets/50e36486-5cf6-4dcd-8221-6cad23c785b5)

### Step 19: Edit Subnet Association for the 1st VPC
Associate the subnet with the route table.

![image](https://github.com/user-attachments/assets/1151b351-5b57-4095-9910-6f64bca35dd3)

### Step 20: Create Route Table for the 2nd VPC
Create the route table for the 2nd VPC.

![image](https://github.com/user-attachments/assets/0d6c5038-cbd9-4a25-b740-4bd3fde2ccda)

### Step 21: Edit 2nd Route Table - Add Internet Gateway and Transit Gateway
Edit the 2nd route table to add the internet gateway and the Transit Gateway, and provide the CIDR of the other VPCs.

![image](https://github.com/user-attachments/assets/730ea557-307d-4449-aeff-f7716aa5daa7)

### Step 22: Edit Subnet Association for the 2nd VPC
Associate the subnet with the 2nd route table.

![image](https://github.com/user-attachments/assets/7ceb7572-4a53-4a8a-aa03-46ca167e70fb)

### Step 23: Create Route Table for the 3rd VPC
Create the route table for the 3rd VPC.

![image](https://github.com/user-attachments/assets/4d7d2298-8fab-42fc-887e-d4b20996a7dc)

### Step 24: Edit 3rd Route Table - Add Internet Gateway and Transit Gateway
Edit the 3rd route table to add the internet gateway and the Transit Gateway, and provide the CIDR of the other VPCs.

![image](https://github.com/user-attachments/assets/ed16e0b1-2292-40d6-9c9f-415107ff8fa0)

### Step 25: Edit Subnet Association for the 3rd VPC
Associate the subnet with the 3rd route table.

![image](https://github.com/user-attachments/assets/b586c5bd-2165-4ee0-935b-fd43e00a5240)

### Step 26: Launch 1st Instance with Network Configuration
Launch an EC2 instance in the 1st VPC and configure the network.

![image](https://github.com/user-attachments/assets/c0f0c9ab-2663-48b8-88bc-5b19e6c2b20d)

### Step 27: Security Group Rules for the 1st Instance
Set the appropriate security group rules for the 1st instance.

![image](https://github.com/user-attachments/assets/b3aa88ce-8cde-42f2-87c2-69478eb00cb8)

### Step 28: Advanced Details for the 1st Instance
Configure advanced instance details as necessary.

![image](https://github.com/user-attachments/assets/81560871-8490-4430-be8e-547851c3db50)

### Step 29: Launch 2nd Instance with Network Configuration
Launch the EC2 instance in the 2nd VPC with network configuration.

![image](https://github.com/user-attachments/assets/addd432d-2186-4255-9368-9c17cdbbd54b)

### Step 30: Security Group Rules for the 2nd Instance
Set the appropriate security group rules for the 2nd instance.

![image](https://github.com/user-attachments/assets/c99d8b96-ac0f-4575-acb5-4beb565e4410)

### Step 31: Advanced Details for the 2nd Instance
Configure advanced details for the 2nd instance.

![image](https://github.com/user-attachments/assets/a5cd1c32-39f7-4a6e-b0ec-6596d5d71e96)

### Step 32: Launch 3rd Instance with Network Configuration
Launch the EC2 instance in the 3rd VPC with network configuration.

![image](https://github.com/user-attachments/assets/5a2d14ef-5911-4c44-88a5-ac1e628a06ff)

### Step 33: Security Group Rules for the 3rd Instance
Set the appropriate security group rules for the 3rd instance.

![image](https://github.com/user-attachments/assets/fa84033a-e44b-4d86-8882-2ff8c571e0ff)

### Step 34: Advanced Details for the 3rd Instance
Configure advanced details for the 3rd instance.

![image](https://github.com/user-attachments/assets/b145fabd-c939-4608-9b78-aa6e16820a61)

### Step 35: Successfully Launched Three Instances
All three instances are successfully launched.

![image](https://github.com/user-attachments/assets/873251ab-91e5-4d75-a92c-46f77c18ac30)

### Step 36: Connect to the 1st Instance via MobaXterm
Connect to the 1st instance using MobaXterm.

![image](https://github.com/user-attachments/assets/9192542e-737a-4c60-a409-4a731413040a)

### Step 37: Connect to the 2nd Instance via MobaXterm
Connect to the 2nd instance using MobaXterm.

![image](https://github.com/user-attachments/assets/7c4ca62e-0ec2-4376-b6b8-8c41d06b877d)

### Step 38: Connect to the 3rd Instance via MobaXterm
Connect to the 3rd instance using MobaXterm.

![image](https://github.com/user-attachments/assets/ce9878d8-9be2-4492-b7cd-037754607dcc)

### Step 39: Ping Other Instances from 1st Instance
Ping the IPs of the 2nd and 3rd instances from the 1st instance to check communication.

![image](https://github.com/user-attachments/assets/44587a12-ac07-4adc-b787-f8064024016c)

### Step 40: Ping Other Instances from 2nd Instance
Ping the IPs of the 1st and 3rd instances from the 2nd instance.

![image](https://github.com/user-attachments/assets/0fa1a477-72b2-44f8-96e9-d907eb1912cd)

### Step 41: Ping Other Instances from 3rd Instance
Ping the IPs of the 1st and 2nd instances from the 3rd instance.

![image](https://github.com/user-attachments/assets/16706812-017e-46b9-9459-3cee83afe406)


---

## Conclusion

You’ve successfully set up a Transit Gateway in AWS, connected three VPCs, launched instances within each VPC, and verified communication between the instances across the VPCs.

Make sure your security group rules and route tables are configured correctly to allow the necessary traffic for inter-VPC communication.
