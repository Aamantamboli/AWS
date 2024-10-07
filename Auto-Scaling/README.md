<h1>CREATE AUTO SCALING WITH NGINX</h1>

![image](https://github.com/user-attachments/assets/6aa38377-56b3-48bb-aa8c-8863dd689a5f)

<h3>Step 2: Connect and Install NGINX</h3>

```
sudo yum install nginx -y
systemctl start nginx
systemctl enable nginx 
```

<h3>Step 3: Go to action and click on image and template then click on create image </h3>

![image](https://github.com/user-attachments/assets/a41a1fe5-3d12-4b74-8c28-7e3700459e40)

<h3>Step 4: Give name to AMI and create AMI of Instance</h3>

![image](https://github.com/user-attachments/assets/ed8d1060-e353-492f-869d-ad496e3cf048)

<h3>Step 5: Create 1st Template</h3>

```
#!/bin/bash
sudo -i
yum install git -y
git clone https://github.com/Aamantamboli/Auto-Scaling.git
mv Auto-Scaling/todo/* /usr/share/nginx/html
sudo systemctl restart nginx
```

<h3>Step 5: Create 2nd Template</h3>

```
#!/bin/bash
sudo -i
yum install git -y
git clone https://github.com/Aamantamboli/Auto-Scaling.git
mv Auto-Scaling/season/ /usr/share/nginx/html/
sudo systemctl restart nginx
```

<h3>Step 6: Create 3rd Template</h3>

```
#!/bin/bash
sudo -i
yum install git -y
git clone https://github.com/Aamantamboli/Auto-Scaling.git
mv Auto-Scaling/traffic/ /usr/share/nginx/html/
sudo systemctl restart nginx
```

<h3>Succesfully Created Three Teamplate</h3>

![image](https://github.com/user-attachments/assets/c599acff-7826-48d3-ada9-8f31eec7215c)

<h3>Step 7: Create Load Balancer</h3>

![image](https://github.com/user-attachments/assets/7985d6f5-7b0c-497b-9905-7746d39811a4)

<h3>Step 8: Create 1st Target Group and give health check path / </h3>

![image](https://github.com/user-attachments/assets/f32c20f6-f692-4202-b6dd-144d80aa3924)

<h3>Step 9: Create 2nd Target Group and give health check path /season</h3>

![image](https://github.com/user-attachments/assets/c163436f-8951-4ecd-a550-a03e2cdfadaa)

<h3>Step 10: Create 3rd Target Group and give health check path /traffic</h3>

![image](https://github.com/user-attachments/assets/3178a527-08e0-488b-97b8-923a14e7f718)

<h3>Successfully Created three Target Group</h3>

![image](https://github.com/user-attachments/assets/64364260-3bce-4158-8f79-737042239f35)

<h3>Step 11: Add all target group listener to Load Balancer</h3>

![image](https://github.com/user-attachments/assets/8d238440-115e-4a2a-919b-dcda8ee2314e)

![image](https://github.com/user-attachments/assets/efae5a5f-6053-4eec-b7d8-0a58ac6f82a8)

![image](https://github.com/user-attachments/assets/958ed9ba-012a-411f-981d-f218941d9d69)

<h3>Successfully added listener to Load Balancer</h3>

![image](https://github.com/user-attachments/assets/e41ea758-13e1-4a30-b632-5231f321c3be)

<h3>Step 12: Create 1st Auto Scaling Group</h3>

![image](https://github.com/user-attachments/assets/29e098ca-e4be-4627-8f2d-29e39e9f110e)

<h3>Step 13: Attach to Load Balancer</h3>

![image](https://github.com/user-attachments/assets/b0c13b32-0d3f-48fc-b0f3-96892f2c953d)

<h3>Step 14: Create 2nd Auto Scaling Group</h3>

![image](https://github.com/user-attachments/assets/9e57c206-7f83-4079-8fa1-ad2d6e4ddea3)

<h3>Step 15: Attach to Load Balancer</h3>

![image](https://github.com/user-attachments/assets/2ec6440b-5741-400e-bf4a-e322a31f2d54)

<h3>Step 16: Create 3rd Auto Scaling Group</h3>

![image](https://github.com/user-attachments/assets/6461f1d9-df59-4e11-9985-b44e9fd44e35)

<h3>Step 17: Attach to Load Balancer</h3>

![image](https://github.com/user-attachments/assets/b1a6b34a-0fee-4e4e-b86e-5826ca4076a3)

<h3>Successfully Created three Auto Scaling Group</h3>

![image](https://github.com/user-attachments/assets/261e8fa1-07d9-498f-959d-2c64539a99c5)

<h3>Step 18: Paste endpoint of Load Balancer in Browser</h3>

![image](https://github.com/user-attachments/assets/b3364ad5-aba2-4f44-b36d-0474c513afb9)

<h3>Step 19: Paste endpoint of Load Balancer in Browser with :81/season</h3>

![image](https://github.com/user-attachments/assets/32ce1185-ef94-4208-b662-3bdfa36c99fa)

<h3>Step 20: Paste endpoint of Load Balancer in Browser with :82/traffic</h3>

![image](https://github.com/user-attachments/assets/a40d23e9-a569-44f6-8dcd-72890fc1fd5c)
