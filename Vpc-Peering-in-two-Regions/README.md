<h1>Creating VPC peering in two different regions of IP 12.7.0.0/16 & 11.8.0.0/16</h1>

![WhatsApp Image 2024-08-23 at 21 04 10_ba805489](https://github.com/user-attachments/assets/42f86486-4a05-4c6f-860e-ef8c553c648c)

<h3>Step 1: Create a VPC in Mumbai region </h3>

![image](https://github.com/user-attachments/assets/342d56c0-82c6-42ef-9bb4-8527fba3b086)

<h3>Step 2: Create subnet in Mumbai region </h3>

![image](https://github.com/user-attachments/assets/6035b2d3-d5d9-48a0-aff8-a45124a1a5bf)

<h3>Step 3: Create Internet Gateway in Mumbai region</h3>

![image](https://github.com/user-attachments/assets/8bafa048-b1d2-4052-a9e2-1547d4f90a0f)

<h3>Step 4: Attach Internet Gateway to VPC in Mumbai region</h3>

![image](https://github.com/user-attachments/assets/7c9b6e40-0e1b-421d-8c28-c3ada351f9c8)

<h3>Step 5: Launch public instance in Mumbai region</h3>

![image](https://github.com/user-attachments/assets/5e76ff4b-4625-415d-8434-458be01dbb59)

![image](https://github.com/user-attachments/assets/10844f8a-c795-491a-ad2a-3e20a4e3b818)

![image](https://github.com/user-attachments/assets/4a6914b2-6468-4db8-bb4e-bb2852449fad)

![image](https://github.com/user-attachments/assets/8340ee1c-0ada-4c6f-9688-7efbc10a8704)

<h3>Step 6: Edit inbound rules of security group</h3>

![image](https://github.com/user-attachments/assets/1ccdbdc8-ce49-414f-84a2-d5bc205074ae)

<h3>Step 7: Edit routes </h3>

![image](https://github.com/user-attachments/assets/7821de4c-494c-4038-941c-c4bef52580a6)

<h3>Step 8: Edit subnet association </h3>

![image](https://github.com/user-attachments/assets/b410932c-8585-4728-a3d2-8a6d4941662f)

<h3>Step 9: Create a VPC in Osaka region</h3>

![image](https://github.com/user-attachments/assets/226b1385-6ca7-433b-97c4-603805fa35b2)

<h3>Step 10: Create subnet in Osaka region</h3>

![image](https://github.com/user-attachments/assets/19c2caf2-46eb-48bb-ae1a-08ffb014c112)

<h3>Step 11: Launch private instance in Osaka region</h3>

![image](https://github.com/user-attachments/assets/b28a0253-0392-41f0-a71a-8eeb13c1f75b)

![image](https://github.com/user-attachments/assets/398fd32f-6734-479f-9ee4-0ab8f672dddc)

![image](https://github.com/user-attachments/assets/4d293296-eedc-4e66-9272-99ffa6bcfba6)

![image](https://github.com/user-attachments/assets/4eba5967-224d-42eb-a045-a14905af2698)

<h3>Step 12: Edit inbound rules of security group</h3>

![image](https://github.com/user-attachments/assets/1921d671-c899-4247-96b3-ab41d10dd0c3)

<h3>Step 13: Create peering connection in Mumbai region and give VPC id of Osaka region</h3>

![image](https://github.com/user-attachments/assets/72d9d20f-2c61-4941-ae8b-160e5c214c24)

![image](https://github.com/user-attachments/assets/d849e116-58fc-4158-95a3-c493bd8c6559)

<h3>Step 14: Accept request in peering connection in Osaka region</h3>

![image](https://github.com/user-attachments/assets/f21963f2-19fc-4994-a1c4-811641528218)

<h3>Step 15: Create route in Mumbai region</h3>

![image](https://github.com/user-attachments/assets/03b6560b-dce9-48d5-865d-eee5b6fbead2)

<h3>Step 16: Edit route in Mumbai and give cidr of Osaka region VPC and add Internet Gateway</h3>

![image](https://github.com/user-attachments/assets/5819454b-fe6e-43eb-b2d7-660f39105f69)

<h3>Step 17: Edit routes in Tokyo region and give cidr of first region</h3>

![image](https://github.com/user-attachments/assets/92ccee0b-e9e9-4dac-b33e-8d534e3e90c7)

<h3>Step 18: Edit subnet association in Osaka region</h3>

![image](https://github.com/user-attachments/assets/745a12f8-397c-4ba2-b6b5-c9a6b5c5477b)

<h3>Step 19: Open MobaXterm and paste public IP of public instance and upload a private key of public instance and you can communicate with Osaka region</h3>

![image](https://github.com/user-attachments/assets/28aa3343-3551-4b47-bc86-7bc6dac7f3ff)
