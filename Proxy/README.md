# Proxy Setup in AWS

This guide will walk you through setting up a proxy in AWS, using a public EC2 instance to proxy traffic to a private EC2 instance. The private instance will have internet access via the public instance, and we'll set up a simple web application on the private EC2 instance.

---

## Prerequisites

- AWS Account
- Basic knowledge of AWS services (VPC, EC2)
- A working VPC setup with NATting configured (as described in the **NATting** section)

---

## Step 1: Do NATting

Before setting up the proxy, ensure that you've followed the [NATting steps](#natting) to configure your VPC, subnets, and route tables. This will ensure that your private EC2 instance can access the internet through the public EC2 instance.

---

## Step 2: Launch a Public EC2 Instance

1. Go to the **EC2 Dashboard** and launch a new EC2 instance.
2. In the **network settings**, select the **VPC** you created earlier and choose the **public subnet**.
3. Make sure to enable **Auto-assign Public IP** so that the public EC2 instance can be accessed from the internet.

   ![Launch Public EC2 Instance](https://github.com/user-attachments/assets/a9bf12bd-3d8a-4e36-ae97-c50bef90e526)

---

## Step 3: Launch a Private EC2 Instance

1. Launch another EC2 instance, but this time choose the **private subnet**.
2. In the **network settings**, ensure **Auto-assign Public IP** is disabled, as this instance will not have direct internet access.

   ![Launch Private EC2 Instance](https://github.com/user-attachments/assets/9a90ecb8-d466-414d-aced-6f2045f4e3f1)

---

## Step 4: Connect to the Public EC2 Instance

1. Copy the **public IP** of your public EC2 instance.
2. Open **MobaXterm** (or any preferred SSH client) and connect using the **public IP** of the instance and the **key pair** you selected during launch.

   ![Connect to Public EC2 Instance](https://github.com/user-attachments/assets/a65397bc-b84e-4f7b-9c3b-c93cc133c165)

---

## Step 5: Upload Your SSH Key

1. Ensure the correct **key pair** file is uploaded to your SSH client to authenticate the connection.

   ![Upload SSH Key](https://github.com/user-attachments/assets/9f0f0083-69b6-45a8-b784-c5d2e9530c04)

---

## Step 6: Change the Permission of the Private Key

1. Change the permission of your private key to `400` for security.

2. Use SSH to connect to the **private EC2 instance** by entering its **private IP**.

   ![Change Permissions](https://github.com/user-attachments/assets/be083ceb-e801-4b69-94fe-d97b30716701)

---

## Step 7: Successfully Login into the Private Instance and Enable Internet Access

1. Once logged into the private EC2 instance, you can configure it to access the internet via the NAT setup.

   ![Login to Private Instance](https://github.com/user-attachments/assets/ea20b781-0de8-437a-a4c1-5439294085f7)

---

## Step 8: Install and Setup Application on the Private Instance

1. Run the following commands to download and configure a Tomcat web server and a simple web application:

```bash
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

---

## Step 9: Set Up Nginx on the Public EC2 Instance

1. On the **public EC2 instance**, install **Nginx** to act as a proxy for the private instance.

```bash
yum install nginx -y
vim /etc/nginx/nginx.conf
```

2. Modify the **nginx.conf** file to point to the private instance (details on configuration are beyond this guide, but it should be a basic reverse proxy configuration).

   ![Nginx Configuration](https://github.com/user-attachments/assets/81f07963-8b3f-4538-bcda-8ca42fae6b1e)

3. Start **Nginx**:

```bash
systemctl start nginx
```

---

## Step 10: Test the Proxy Setup

1. Open a web browser and paste the **public IP** of the public EC2 instance.
2. You should now be able to access the application running on the private EC2 instance through the public EC2 instance as a proxy.

   ![Test Proxy](https://github.com/user-attachments/assets/f79959b3-e4b8-4909-9bc6-aa62c3a9f789)

---

## Security Group Settings

Make sure the following ports are open in the **Security Group** for both instances:

- **SSH (port 22)** – For SSH access.
- **HTTP (port 80)** – For web traffic.
- **HTTPS (port 443)** – If your application uses HTTPS.
- **TCP (port 3000 or any other required ports)** – For other required services.

---

## Conclusion

You have successfully set up a proxy configuration in AWS, where the public EC2 instance proxies traffic to the private EC2 instance, allowing the private instance to access the internet and host an application.

---

### References
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/)
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [Nginx Reverse Proxy Setup](https://www.nginx.com/resources/wiki/start/)
```
