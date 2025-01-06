# Create Auto Scaling with NGINX

This guide will walk you through the steps to set up auto-scaling with NGINX in an AWS environment. It includes setting up NGINX, creating AMIs, configuring target groups, load balancers, and auto-scaling groups.

---

## Step 1: Install and Start NGINX

Connect to your instance and install NGINX with the following commands:

```bash
sudo yum install nginx -y
systemctl start nginx
systemctl enable nginx
```

---

## Step 2: Create an AMI of Your Instance

1. Go to the **Actions** section of your instance.
2. Click on **Image and Templates**, then click **Create Image**.
3. Name the AMI and create it from your instance.

---

## Step 3: Create Custom Templates for NGINX Setup

### 3.1: First Template - For Todo Page

```bash
#!/bin/bash
sudo -i
yum install git -y
git clone https://github.com/Aamantamboli/Auto-Scaling.git
mv Auto-Scaling/todo/* /usr/share/nginx/html
sudo systemctl restart nginx
```

### 3.2: Second Template - For Season Page

```bash
#!/bin/bash
sudo -i
yum install git -y
git clone https://github.com/Aamantamboli/Auto-Scaling.git
mv Auto-Scaling/season/ /usr/share/nginx/html/
sudo systemctl restart nginx
```

### 3.3: Third Template - For Traffic Page

```bash
#!/bin/bash
sudo -i
yum install git -y
git clone https://github.com/Aamantamboli/Auto-Scaling.git
mv Auto-Scaling/traffic/ /usr/share/nginx/html/
sudo systemctl restart nginx
```

---

### Successfully Created Three Templates

---

## Step 4: Create Load Balancer

1. Go to the **EC2 Dashboard** and select **Load Balancers**.
2. Create a new **Application Load Balancer** (ALB).

---

## Step 5: Create Target Groups

### 5.1: Create First Target Group

Set the health check path to `/`.

### 5.2: Create Second Target Group

Set the health check path to `/season`.

### 5.3: Create Third Target Group

Set the health check path to `/traffic`.

---

### Successfully Created Three Target Groups

---

## Step 6: Add Target Groups as Listeners to the Load Balancer

1. Add each target group to the **Load Balancer** as a listener for different paths.

---

### Successfully Added Listeners to Load Balancer

---

## Step 7: Create Auto Scaling Groups

### 7.1: Create First Auto Scaling Group

### 7.2: Attach First Auto Scaling Group to Load Balancer

### 7.3: Create Second Auto Scaling Group

### 7.4: Attach Second Auto Scaling Group to Load Balancer

### 7.5: Create Third Auto Scaling Group

### 7.6: Attach Third Auto Scaling Group to Load Balancer

---

### Successfully Created Three Auto Scaling Groups

---

## Step 8: Test the Load Balancer Endpoints in the Browser

### 8.1: Test the Default Load Balancer Endpoint

Paste the endpoint of the Load Balancer in your browser to test the default page.

### 8.2: Test the `/season` Path

Append `:81/season` to the Load Balancer endpoint in the browser.

### 8.3: Test the `/traffic` Path

Append `:82/traffic` to the Load Balancer endpoint in the browser.

---

### Conclusion

Congratulations! You've successfully set up auto-scaling with NGINX on AWS using Application Load Balancers and Auto Scaling Groups. This setup ensures that your web application scales dynamically based on demand, providing better availability and performance.
