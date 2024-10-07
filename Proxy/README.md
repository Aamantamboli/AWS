<h1>PROXY</h1>
<h3>Step 1: Do Natting</h3>
<h3>Step 2: Launch public EC2 instance go to network setting select VPC which we created and select public subnet and auto assign public IP </h3>

![image](https://github.com/user-attachments/assets/a9bf12bd-3d8a-4e36-ae97-c50bef90e526)

<h3>Step 3: Launch private EC2 instance go to network setting select VPC which we created and select private subnet and auto assign public IP disable</h3>

![image](https://github.com/user-attachments/assets/9a90ecb8-d466-414d-aced-6f2045f4e3f1)

<h3>Step 4: Copy public IP and paste in MobaXterm and select your key</h3>

![image](https://github.com/user-attachments/assets/a65397bc-b84e-4f7b-9c3b-c93cc133c165)

<h3>Step 5: Upload your key</h3>

![image](https://github.com/user-attachments/assets/9f0f0083-69b6-45a8-b784-c5d2e9530c04)

<h3>Step 6: Change permission of file to 400 and by ssh connection paste private IP of private instance</h3>

![image](https://github.com/user-attachments/assets/be083ceb-e801-4b69-94fe-d97b30716701)

<h3>Step 7: Successfully login into private instance and given internet access to it </h3>

![image](https://github.com/user-attachments/assets/ea20b781-0de8-437a-a4c1-5439294085f7)

<h3>Step 8: Connect private instance</h3>

```
curl -O https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz
tar -xvf apache-tomcat-9.0.93.tar.gz
yum install git -y
git clone https://github.com/Aamantamboli/student.git
sudo mv apache-tomcat-9.0.93 /opt/
sudo mv student/student.war /opt/apache-tomcat-9.0.93/webapps/
sudo yum install java-1.8.0-amazon-corretto-devel.x86_64 -y
cd /opt/apache-tomcat-9.0.93/
bash bin/catalina.sh start
```

<h3>Step 9: Connect public instance</h3>

```
yum install nginx -y
vim /etc/nginx/nginx.conf  
```

![image](https://github.com/user-attachments/assets/81f07963-8b3f-4538-bcda-8ca42fae6b1e)

```
systemctl start nginx
```

<h3>Step 10: Paste public IP of public instance </h3>

![image](https://github.com/user-attachments/assets/f79959b3-e4b8-4909-9bc6-aa62c3a9f789)

**Must have (SSH,HTTP,HTTPS,TCP) Port in Security Group**
