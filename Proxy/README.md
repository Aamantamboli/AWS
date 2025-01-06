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

![image](https://github.com/user-attachments/assets/23ac37fa-0e40-407f-ac75-c01c96b16936)

---

## Step 3: Launch a Private EC2 Instance

1. Launch another EC2 instance, but this time choose the **private subnet**.
2. In the **network settings**, ensure **Auto-assign Public IP** is disabled, as this instance will not have direct internet access.

![image](https://github.com/user-attachments/assets/ccd34e90-b2c3-4ebd-b73f-33fc9872bc28)

---

## Step 4: Connect to the Public EC2 Instance

1. Copy the **public IP** of your public EC2 instance.
2. Open **MobaXterm** (or any preferred SSH client) and connect using the **public IP** of the instance and the **key pair** you selected during launch.

![image](https://github.com/user-attachments/assets/d53236b9-26e8-4ad9-b7ed-0e14b2ba89e6)

---

## Step 5: Upload Your SSH Key

1. Ensure the correct **key pair** file is uploaded to your SSH client to authenticate the connection.

![image](https://github.com/user-attachments/assets/0aa3ab03-0cb1-4026-98eb-4db0cef20de6)

---

## Step 6: Change the Permission of the Private Key

1. Change the permission of your private key to `400` for security.

2. Use SSH to connect to the **private EC2 instance** by entering its **private IP**.

![image](https://github.com/user-attachments/assets/9af159ef-715b-428d-979d-4102c7c818f4)

---

## Step 7: Successfully Login into the Private Instance and Enable Internet Access

1. Once logged into the private EC2 instance, you can configure it to access the internet via the NAT setup.

![image](https://github.com/user-attachments/assets/8c7265e5-9bbf-448e-bc92-67324a650bd1)

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

![image](https://github.com/user-attachments/assets/7623ff86-a9ab-4712-93b2-79a622929401)

3. Start **Nginx**:

```bash
systemctl start nginx
```

---

## Step 10: Test the Proxy Setup

1. Open a web browser and paste the **public IP** of the public EC2 instance.
2. You should now be able to access the application running on the private EC2 instance through the public EC2 instance as a proxy.

![image](https://github.com/user-attachments/assets/a0b433ab-aeec-4689-8c4a-5e68c98232a6)

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
