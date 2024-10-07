<h1>Natting</h1>
<h3>Step 1: Create a VPC</h3>        

![image](https://github.com/user-attachments/assets/ef8820d6-0b6e-4c2d-98d8-6758d0c418e0)

<h3>Step 2: Create two Subnet public and private</h3>

![image](https://github.com/user-attachments/assets/9ae3fb3c-bbb2-4290-8910-7f960d8dcb0d)

![image](https://github.com/user-attachments/assets/3bbe5b1d-547c-4374-a2f8-7f2ad69974e5)

![image](https://github.com/user-attachments/assets/f7f73ddd-6e6d-46dd-a849-257352d2d4be)

<h3>Step 3: .Create Internet Gateway and attach  to VPC and select your VPC </h3>

![image](https://github.com/user-attachments/assets/e94d4e0a-df65-49b3-be75-a9153c3228bf)

<h3>Step 4: Create Nat Gateway and select public subnet and allocate elastic IP</h3>

![image](https://github.com/user-attachments/assets/f3c99e1c-e521-40c5-a58b-188fdab7bcd7)

<h3>Step 5: Create a route table for public </h3>

![image](https://github.com/user-attachments/assets/a24f7b42-a134-48fb-a7c4-b5653ecd75d8)

<h3>Step 6: Edit route table and add internet gateway in it </h3>

![image](https://github.com/user-attachments/assets/10946d0e-d55e-4b36-8cdb-8c99c1ccbe71)

<h3>Step 7: Edit subnet associations and select public subnet </h3>

![image](https://github.com/user-attachments/assets/799f3cd5-d415-4d20-8309-b4c116e1be64)

<h3>Step 8: Create route table for private </h3>

![image](https://github.com/user-attachments/assets/bc2380dd-3437-4c14-ab8c-0215fe610f5d)

<h3>Step 9: Edit route table and add Nat gateway in it</h3>

![image](https://github.com/user-attachments/assets/47757377-42dc-400c-a674-2619d14b1d82)

<h3>Step 10: Edit subnet associations and select private subnet</h3>

![image](https://github.com/user-attachments/assets/c95ec220-a5c3-41a1-8b21-758cf92f221f)

<h3>Step 11: Launch public EC2 instance go to network setting select VPC which we created and select public subnet and auto assign public IP enable </h3>

![image](https://github.com/user-attachments/assets/e6d96cb0-5702-4a35-acd1-1bea6f1c4cca)

<h3>Step 12: Launch private EC2 instance go to network setting select VPC which we created and select private subnet and auto assign public IP disable </h3>

![image](https://github.com/user-attachments/assets/0099b897-a8e2-4ea2-8287-050d8ea8435a)

<h3>Step 13: Copy public IP and paste in mobaxterm and select your key</h3>

![image](https://github.com/user-attachments/assets/b39b558a-22b9-4ac2-93c2-93f2e16673c1)

<h3>Step 14: Upload your key</h3>

![image](https://github.com/user-attachments/assets/bbf73dfd-6cc0-4636-aa85-70835ac36fbe)

<h3>Step 15: Change permission of file to 400 and by ssh connection paste private IP of private instance</h3>

![image](https://github.com/user-attachments/assets/5ee93db1-89fc-4cfc-bd58-fd796c1f0f65)

<h3>Step 16: Successfully login into private instance and give internet access to it </h3>

![image](https://github.com/user-attachments/assets/5e948089-f494-4ffc-9c71-e8ae5daec6ff)

**Must have (SSH,HTTP,HTTPS,TCP) port in security group**
