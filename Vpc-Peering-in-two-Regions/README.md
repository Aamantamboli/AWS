# VPC Peering in AWS Between Mumbai and Osaka Regions

This guide walks you through the steps to set up a VPC peering connection between two different AWS regions: Mumbai (ap-south-1) and Osaka (ap-northeast-3), with CIDR blocks `12.7.0.0/16` (Mumbai) and `11.8.0.0/16` (Osaka).

![image](https://github.com/user-attachments/assets/4b7302de-c224-46a1-b112-40f8f997f650)

## Steps

### Step 1: Create a VPC in the Mumbai region

1. Go to the **VPC Dashboard** in the Mumbai region.
2. Click **Create VPC** and provide the CIDR block `12.7.0.0/16`.
3. Configure other settings as needed (e.g., DNS support) and create the VPC.

![image](https://github.com/user-attachments/assets/c7bd2b93-c6b3-45af-a7ea-cd6e176da942)

---

### Step 2: Create a Subnet in the Mumbai region

1. In the **VPC Dashboard**, create a subnet within the VPC you just created.
2. Assign an appropriate CIDR block (e.g., `12.7.1.0/24`).

![image](https://github.com/user-attachments/assets/d1b373fe-187c-4024-96de-66f40bc18db2)

---

### Step 3: Create an Internet Gateway in the Mumbai region

1. Go to the **Internet Gateways** section in the **VPC Dashboard**.
2. Create a new Internet Gateway and name it appropriately.

![image](https://github.com/user-attachments/assets/2f95a269-3c65-4f2c-94a9-2a763c007f07)

---

### Step 4: Attach the Internet Gateway to the VPC in Mumbai region

1. After creating the Internet Gateway, select it and click **Attach to VPC**.
2. Select the VPC you created in Step 1.

![image](https://github.com/user-attachments/assets/1a59a675-6937-4ef8-858c-a7bfd7c79e51)

---

### Step 5: Launch a Public Instance in the Mumbai region

1. Launch an EC2 instance in the Mumbai region using the subnet you created.
2. Ensure it has a **Public IP** and select a security group that allows inbound SSH (port 22) access.

![image](https://github.com/user-attachments/assets/158412c4-178c-4f58-be83-ddc676f090a1)
![image](https://github.com/user-attachments/assets/dccc9105-3982-4669-b854-5dc9b0225404)
![image](https://github.com/user-attachments/assets/a32a8cdd-6427-41ff-8e1f-2898ce7fe6dc)
![image](https://github.com/user-attachments/assets/cd6f41a0-3d64-43a7-aa4a-374c9d0ff023)

---

### Step 6: Edit the Inbound Rules of the Security Group

1. Navigate to the **Security Groups** section.
2. Add an inbound rule to allow SSH traffic (port 22) from your IP address.

![image](https://github.com/user-attachments/assets/0ddf73c9-2803-423f-bb66-b5eb66fb3d7f)

---

### Step 7: Edit Routes in the Mumbai region

1. Go to the **Route Tables** section and select the route table associated with your subnet.
2. Add a route for outbound traffic to the internet (0.0.0.0/0) through the Internet Gateway.

![image](https://github.com/user-attachments/assets/3121e013-d04c-4b65-b306-12a80b968abf)

---

### Step 8: Edit Subnet Association

1. Ensure that your subnet is associated with the correct route table to allow internet access.

![image](https://github.com/user-attachments/assets/88593ab0-b4eb-45b6-93b7-5221591d4768)

---

### Step 9: Create a VPC in the Osaka region

1. Go to the **VPC Dashboard** in the Osaka region.
2. Click **Create VPC** and provide the CIDR block `11.8.0.0/16`.
3. Configure other settings as needed.

![image](https://github.com/user-attachments/assets/1f253e30-603c-4bff-9499-662716263103)

---

### Step 10: Create a Subnet in the Osaka region

1. In the **VPC Dashboard**, create a subnet within the Osaka VPC.
2. Assign a CIDR block (e.g., `11.8.1.0/24`).

![image](https://github.com/user-attachments/assets/dfe73667-4a4b-469c-86fc-6b2eb14bf58c)

---

### Step 11: Launch a Private Instance in the Osaka region

1. Launch an EC2 instance in the Osaka region using the subnet you created.
2. Ensure that the instance is private and does not have a public IP.

![image](https://github.com/user-attachments/assets/9856314c-25cf-4ec7-ac05-f11e6e91847a)
![image](https://github.com/user-attachments/assets/60200ddf-1b42-4a9b-bce8-f6f04c8e7cc5)
![image](https://github.com/user-attachments/assets/fef5994a-4b37-421c-a8cd-d8ff2aa28bc9)
![image](https://github.com/user-attachments/assets/8d13978c-3340-49b9-bad2-72297929d0e9)

---

### Step 12: Edit Inbound Rules of the Security Group

1. Add an inbound rule to allow SSH (port 22) from the IP address of the Mumbai instance (or CIDR block of the Mumbai subnet).

![image](https://github.com/user-attachments/assets/572a5106-7190-4d43-bc62-9fbe26eeb5b6)

---

### Step 13: Create Peering Connection in the Mumbai region

1. In the **VPC Dashboard** in Mumbai, go to **Peering Connections** and click **Create Peering Connection**.
2. Provide the VPC ID of the Osaka region and select the appropriate options.

![image](https://github.com/user-attachments/assets/4f96e4ad-f532-4d4d-b622-d319c8f5ebe2)
![image](https://github.com/user-attachments/assets/3955f843-c814-4a00-b778-d681c712ecaf)

---

### Step 14: Accept Peering Request in the Osaka region

1. Go to the **Peering Connections** section in the Osaka region.
2. Select the pending request and click **Accept**.

![image](https://github.com/user-attachments/assets/63933fca-656b-4e71-8c51-4abc4396cb45)

---

### Step 15: Create a Route in Mumbai Region for Peering Connection

1. In the **Route Tables** section of the Mumbai region, add a route for the CIDR block of the Osaka VPC (`11.8.0.0/16`) pointing to the peering connection.

![image](https://github.com/user-attachments/assets/89a3978b-6eb6-406d-80b7-d12f73c7141f)

---

### Step 16: Edit Routes in Mumbai Region to Add Osaka VPC CIDR

1. In the **Route Tables** section of the Mumbai region, edit the route to include the CIDR block `11.8.0.0/16` and select the peering connection as the target.

![image](https://github.com/user-attachments/assets/f15e6783-dfb5-43a4-bdcb-80829402ade7)

---

### Step 17: Edit Routes in Osaka Region to Add Mumbai VPC CIDR

1. In the **Route Tables** section of the Osaka region, add a route for the CIDR block `12.7.0.0/16` pointing to the peering connection.

![image](https://github.com/user-attachments/assets/09263a32-0408-40dd-9daf-7d547e142bc4)

---

### Step 18: Edit Subnet Association in Osaka Region

1. Ensure the correct subnet in the Osaka region is associated with the right route table to enable communication over the peering connection.

![image](https://github.com/user-attachments/assets/415f4a9a-950f-41ed-b5ca-f24cc435d01f)

---

### Step 19: Test Connectivity Using MobaXterm

1. Open **MobaXterm** and use the public IP of the Mumbai instance to SSH into it.
2. Use the private key associated with the Mumbai instance to establish the SSH connection.
3. You should now be able to communicate with the private instance in the Osaka region.

![image](https://github.com/user-attachments/assets/ae163846-62ff-4973-b399-cde21947ba75)

---

## Conclusion

You have successfully set up a VPC peering connection between

 the Mumbai and Osaka regions. Your instances in both regions should now be able to communicate with each other securely over the peering connection.

Make sure to test the connectivity by initiating an SSH session from your public instance in Mumbai to your private instance in Osaka. If you encounter any issues, check the route tables, security group settings, and subnet associations to ensure everything is configured correctly.

---

## Additional Resources

- [AWS VPC Peering Documentation](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)
- [AWS Security Groups Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- [AWS Route Tables Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
