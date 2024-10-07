# TRANSIT GATEWAY IN SAME REGION
## Step 1: Create 1st  VPC(VIRTUAL PRIVATE CLOUD)
![image](https://github.com/user-attachments/assets/2eacb06a-611a-4a1a-9cb5-0a2203fb0008)
## Step 2: Create one subnet for 1st  VPC
![image](https://github.com/user-attachments/assets/44328c90-60d5-46d5-9507-d3980ba157a5)
## Step 3: Create 1st Internet Gateway
![image](https://github.com/user-attachments/assets/50d33e4d-fcc1-49c0-b8f2-29c5abfac3bb)
## Step 4: Attach 1st Internet Gateway to 1st VPC
![image](https://github.com/user-attachments/assets/47de24cf-d1bd-4d36-b0cd-0711989ea5dc)
## Step 5: Create 2nd  VPC(VIRTUAL PRIVATE CLOUD) 
![image](https://github.com/user-attachments/assets/a991365c-eb7c-483c-9b5e-cf7579c85fc5)
## Step 6: Create one subnet for 2nd  VPC
![image](https://github.com/user-attachments/assets/52a3f5b9-5061-4e26-836a-5c5a55556177)
## Step 7: Create 2nd Internet Gateway
![image](https://github.com/user-attachments/assets/33b5dcbf-1275-4863-84bb-37eaf0d64b57)
## Step 8: Attach 2nd Internet Gateway to 2nd VPC
![image](https://github.com/user-attachments/assets/1aefa15f-5fae-4d84-af1f-ca1b9ecc2278)
## Step 9: Create 3rd VPC(VIRTUAL PRIVATE CLOUD)
![image](https://github.com/user-attachments/assets/908ec941-ffa9-4ad6-8ed2-bf5d0cc01dd5)
## Step 10: Create one subnet for 3rd VPC
![image](https://github.com/user-attachments/assets/66daf186-68dd-48d8-91d8-399b74caa775)
## Step 11: Create 3rd Internet Gateway
![image](https://github.com/user-attachments/assets/1cdd4faf-277f-42db-be9e-fc28dcea7f79)
## Step 12: Attach 3rd Internet Gateway to 3rd VPC
![image](https://github.com/user-attachments/assets/c2677e92-b98b-4153-8a8c-60c61c879076)
## Step 13: Create Transit Gateway
![image](https://github.com/user-attachments/assets/8ae08a50-5489-4eba-b1de-76ab5883addc)
## Step 14: Create Transit Gateway Attachment 1st 
![image](https://github.com/user-attachments/assets/f5bd3e03-7288-464b-8324-442291116093)
## Step 15: Create Transit Gateway Attachment 2nd 
![image](https://github.com/user-attachments/assets/19f01b6a-0671-4156-8fc3-e3f600dd021b)
## Step 16: Create Transit Gateway Attachment 3rd
![image](https://github.com/user-attachments/assets/13c9dd35-0ba9-4866-81b7-4c0c6e3afc3e)
## Step 17: Create Route Table 1st 
![image](https://github.com/user-attachments/assets/8e2c1056-be58-41ff-970d-3770c7430d31)
## Step 18: Edit 1st Route Table add Internet Gateway and add Transit Gateway and give the CIDR of other two VPC’s
![image](https://github.com/user-attachments/assets/22cc74af-3d4c-49e3-89d0-cb720e1f3e45)
## Step 19: Edit Subnet Association and select your subnet
![image](https://github.com/user-attachments/assets/0370b9a2-31a2-4154-b50d-642b5bd43226)
## Step 20: Create Route Table 1st 
![image](https://github.com/user-attachments/assets/99b021a7-ab11-4655-9ce2-95aa1848e01b)
## Step 21: Edit 2nd Route Table add Internet Gateway and add Transit Gateway and give the CIDR of other two VPC’s
![image](https://github.com/user-attachments/assets/8749da18-0fa9-4df9-8877-573f5eaf098d)
## Step 22: Edit Subnet Association and select your subnet
![image](https://github.com/user-attachments/assets/0391da1c-facd-4403-9b6f-e136d8d0a223)
## Step 23: Create Route Table 3rd 
![image](https://github.com/user-attachments/assets/191d022a-c838-4147-8f2d-529fcd0e5dc7)
## Step 24: Edit 3rd Route Table add Internet Gateway and add Transit Gateway and give the CIDR of other two VPC’s
![image](https://github.com/user-attachments/assets/3d1388dd-57b1-4d12-a4b0-0ee42fa1e309)
## Step 25: Edit Subnet Association and select your subnet
![image](https://github.com/user-attachments/assets/f85cb777-cc17-4bcc-8fe7-dcaacd1dcde8)
## Step 26: Launch Instance 1st with network configuration
![image](https://github.com/user-attachments/assets/c650654d-f2c7-4b93-9a22-1794ba850d67)
## Step 27: Security Group Rules 
![image](https://github.com/user-attachments/assets/1bd59d13-6536-40fc-a1fd-64c935272067)
## Step 28: Advance details
![image](https://github.com/user-attachments/assets/20896c1b-08d9-4bb8-bf6c-b8f80ac7be0a)
## Step 29: Launch Instance 2nd with network configuration
![image](https://github.com/user-attachments/assets/dad53dfd-4afa-46d8-9aae-df84b5eecd3f)
## Step 30: Security Group Rules 
![image](https://github.com/user-attachments/assets/ab71545a-000d-4dba-bb4e-79240bca4c3f)
## Step 31: Advance details
![image](https://github.com/user-attachments/assets/1c68a1ba-45f2-4bba-a1da-b9123debb41f)
## Step 32: Launch Instance 3rd with network configuration
![image](https://github.com/user-attachments/assets/018b915e-a8aa-4682-8211-6ceb2e9e33e1)
## Step 33: Security Group Rules
![image](https://github.com/user-attachments/assets/4db6337b-bde6-4f6b-826a-ea3048503546)
## Step 34: Advance details
![image](https://github.com/user-attachments/assets/8235e4fe-2430-4439-af1c-a75e57ebf6c0)
## Step 35: Succesfully Launched three Instance
![image](https://github.com/user-attachments/assets/abce4bb4-a689-414e-a2ab-c544590df225)
## Step 36: Connect 1st Instance through MobaXterm
![image](https://github.com/user-attachments/assets/6eaedb6e-42bb-4a46-89e3-a79d847f0718)
## Step 37: Connect 2nd Instance through MobaXterm
![image](https://github.com/user-attachments/assets/276727a5-3482-49b7-9410-578041e869d5)
## Step 38: Connect 3rd Instance through MobaXterm
![image](https://github.com/user-attachments/assets/ef0cc771-7331-4257-8393-3e223f3f9b3c)
## Step 39: Now ping other two instance IP from 1st instance to check the communication 
![image](https://github.com/user-attachments/assets/bd2c67d2-5e62-4bbc-b953-450390ff5787)
## Step 40: Now ping other two instance IP from 2nd instance to check the communication
![image](https://github.com/user-attachments/assets/9e81a7f4-33ba-4e3e-b911-9804ffb6ea32)
## Step 41: Now ping other two instance IP from 3rd instance to check the communication
![image](https://github.com/user-attachments/assets/fdcf03ff-52e1-4424-85f4-27842873fdc4)
