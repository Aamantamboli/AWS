# Static Web Hosting on EC2 with Nginx

This guide walks you through the steps to set up a static website using an EC2 instance and Nginx web server.

---

## Prerequisites

- AWS Account
- EC2 Instance (Amazon Linux 2 or similar)
- SSH Key Pair for accessing the EC2 instance
- Basic knowledge of EC2 and Nginx

---

## Step 1: Create EC2 Instance and Connect

1. Launch a new EC2 instance from the AWS Console.
2. Connect to your EC2 instance using SSH.

![image](https://github.com/user-attachments/assets/dd533851-4d29-464e-93d6-9f2be27e64d3)

---

## Step 2: Switch to Root User

To perform administrative tasks, switch to the root user:

```bash
sudo -i
```

---

## Step 3: Download the Static Website and Unzip It

1. Download a free static website template from the internet. In this case, we will use a template from Free CSS.
2. Unzip the downloaded file.

```bash
curl -O https://www.free-css.com/assets/files/free-css-templates/download/page296/oxer.zip
unzip oxer.zip
```

---

## Step 4: Install Nginx

1. Install Nginx on the EC2 instance:

```bash
yum install nginx -y
```

2. Check the status of Nginx to ensure it's installed:

```bash
systemctl status nginx
```

3. Start and enable Nginx to run on boot:

```bash
systemctl start nginx
systemctl restart nginx
```

---

## Step 5: Move Unzipped Website Files to Nginx Directory

1. Move the contents of the unzipped website to Nginx's default directory for serving static files:

```bash
mv /path/to/unzipped/files/* /usr/share/nginx/html/
```

Make sure to replace `/path/to/unzipped/files/` with the actual path where the files were unzipped.

---

## Step 6: Access the Static Website

1. In your browser, enter the public IP address of your EC2 instance.
2. The static website should load.

![image](https://github.com/user-attachments/assets/40aafd81-5b01-4bda-a34c-873886a62cb0)

---

## Important Notes

- **Security Group Settings**: Make sure the security group attached to your EC2 instance allows inbound traffic on the **SSH** (port 22) and **HTTP** (port 80) ports.
  
---

## Conclusion

You have successfully set up a static website hosted on an EC2 instance using Nginx. This setup is ideal for serving static content such as HTML, CSS, JavaScript, and image files.

---

## References

- [Amazon EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [Nginx Documentation](https://nginx.org/en/docs/)
