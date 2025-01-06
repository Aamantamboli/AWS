# Hosted Three Microservices: Todo, Student, and Employees - Redirected to Index Page

This guide will take you through the steps to host three microservices (`todo`, `student`, and `employees`) on EC2 instances, set up application load balancing, and then redirect users to the index page with links to these microservices.

---

## Prerequisites

- AWS Account
- EC2 Instances for hosting the microservices
- Application Load Balancer for distributing traffic
- S3 Bucket for hosting the index page
- Route 53 for custom domain setup (optional)

---

## 1st Microservice - Todo Application

### Step 1: Create EC2 Instance

Launch an EC2 instance (Amazon Linux 2) for the `todo` microservice.

![image](https://github.com/user-attachments/assets/e0f6ea89-e814-4c60-a1e2-76db7d005046)

### Step 2: Connect to the EC2 Instance and Set Up Todo Application

Run the following commands to install necessary dependencies, clone the application, and start the web server:

```bash
sudo yum install httpd -y
sudo yum install git -y
git clone https://github.com/Aamantamboli/application.git
sudo mv application/todo/ /var/www/html/
sudo systemctl enable httpd
sudo systemctl start httpd
```

### Step 3: Create Application Load Balancer for 1st Microservice

Create an Application Load Balancer to distribute traffic to the Todo microservice.

![image](https://github.com/user-attachments/assets/986cb36a-f009-44fe-b739-794803a0dc79)

### Step 4: Create Target Group for Todo Service

![image](https://github.com/user-attachments/assets/93e3fa80-e373-4fff-8913-47dca6b7a148)

### Step 5: Provide Health Check Path for Todo Service

Specify the health check path for the target group.

![image](https://github.com/user-attachments/assets/418b3e7a-ab7d-442b-bb52-85393c75536d)

### Step 6: Register Target with Load Balancer

Register the EC2 instance running the `todo` service with the load balancer.

![image](https://github.com/user-attachments/assets/1bd73e1d-ba7b-408f-ac72-ecced4e3e4fa)

### Step 7: Add Listener to Load Balancer

Add the appropriate listener to the load balancer.

![image](https://github.com/user-attachments/assets/a8dd38b8-043e-4518-8c04-458ccc288966)

---

## 2nd Microservice - Student Application

### Step 1: Create RDS (Relational Database Service) and Select MariaDB

Launch an RDS instance with MariaDB to store student data.

![image](https://github.com/user-attachments/assets/4df8b85e-d541-4311-966e-aa786099dc6e)

### Step 2: Set up Database Credentials and Create a New Database

Create a new password and set up the database.

![image](https://github.com/user-attachments/assets/e2f935c8-a409-4e1b-abf8-205132844ad4)

![image](https://github.com/user-attachments/assets/a4d1b40a-cce5-4f57-b2ad-14250c055880)

### Step 3: Set Up Tomcat and Student Application

Download and set up Tomcat, configure the database, and deploy the student application.

```bash
curl -O https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz
tar -xvf apache-tomcat-9.0.93.tar.gz
sudo mv apache-tomcat-9.0.93 /opt/
sudo mv student.war /opt/apache-tomcat-9.0.93/webapps/
sudo mv mysql-connector.jar /opt/apache-tomcat-9.0.93/lib/
sudo yum install java-1.8.0-amazon-corretto-devel.x86_64 -y
cd /opt/apache-tomcat-9.0.93/
vim conf/context.xml
```

### Step 4: Edit the `context.xml` for Database Connection

Edit the `context.xml` file with your database username, password, and endpoint.

```xml
<Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
           maxTotal="100" maxIdle="30" maxWaitMillis="10000"
           username="<username>" password="<password>" driverClassName="com.mysql.jdbc.Driver"
           url="jdbc:mysql://<database_endpoint>:3306/<db_name>"/>
```

### Step 5: Install MariaDB and Set Up Database

Install MariaDB and create the necessary database and table.

```bash
sudo yum install mariadb105.x86_64 -y
mysql -h <database_endpoint> -u <username> -p<password>
create database <db_name>;
use <db_name>;
CREATE TABLE if not exists students(
  student_id INT NOT NULL AUTO_INCREMENT,
  student_name VARCHAR(100) NOT NULL,
  student_addr VARCHAR(100) NOT NULL,
  student_age VARCHAR(3) NOT NULL,
  student_qual VARCHAR(20) NOT NULL,
  student_percent VARCHAR(10) NOT NULL,
  student_year_passed VARCHAR(10) NOT NULL,
  PRIMARY KEY (student_id)
);
exit
bash bin/catalina.sh start
```

### Step 6: Create Application Load Balancer for 2nd Microservice

Create an Application Load Balancer for the `student` service.

![image](https://github.com/user-attachments/assets/7752f3e3-f458-4f92-9e19-9c7325aadcd2)

### Step 7: Create Target Group for Student Service

![image](https://github.com/user-attachments/assets/e66d0b90-5eea-46a7-911e-a8f5a643d446)

### Step 8: Add Health Check Path for Student Service

![image](https://github.com/user-attachments/assets/c778c1e1-9831-461b-9df8-7d2ee0add9c3)

### Step 9: Register Target for Student Service

![image](https://github.com/user-attachments/assets/8179a342-c7c8-466a-95fa-3f5f099a7cea)

### Step 10: Add Listener for Load Balancer

![image](https://github.com/user-attachments/assets/37115c1e-5329-4400-baa4-73d3fc2acef9)

**Ensure that TCP port 8080 is open in the security group.**

---

## 3rd Microservice - Employees Application

### Step 1: Launch Frontend EC2 Instance

Launch an EC2 instance for the frontend of the `employees` microservice.

![image](https://github.com/user-attachments/assets/62e9f376-b1f7-4875-88b6-b645f0003230)

### Step 2: Launch Backend EC2 Instance and Set Up PostgreSQL

Launch an EC2 instance for the backend and install PostgreSQL.

![image](https://github.com/user-attachments/assets/08a3684d-ed41-48a5-b927-88b02dcfd816)

### Step 3: Connect Frontend EC2 and Set Up

Install Node.js, npm, and the necessary dependencies for the frontend.

```bash
sudo apt update
sudo apt install -y nodejs npm
sudo npm install -g n
sudo n 14.17.0
sudo apt-get install git-all -y
git clone https://github.com/shubhamkalsait/devops-fullstack-app.git
cd devops-fullstack-app/frontend/
sudo vim .env
REACT_APP_SERVER_URL=http://<backend_pub_ip>:8080/employees
npm install
npm start
```

### Step 4: Connect Backend EC2 and Set Up PostgreSQL

Install PostgreSQL, configure the database, and set up the backend application.

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib -y
sudo passwd postgres
sudo -u postgres psql
CREATE DATABASE employees;
CREATE USER test WITH PASSWORD '1234';
GRANT ALL PRIVILEGES ON DATABASE employees TO test;
\q
exit
```

Install Go and run the backend application.

```bash
sudo curl -O https://dl.google.com/go/go1.19.linux-amd64.tar.gz
sudo tar -xvf go1.19.linux-amd64.tar.gz
sudo mv go /usr/local
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
git clone https://github.com/shubhamkalsait/devops-fullstack-app.git
cd devops-fullstack-app/backend/
sudo DB_HOST=localhost DB_USER=test DB_PASSWORD=1234 DB_NAME=employees DB_PORT=5432 go run main.go
```

### Step 5: Create Network Load Balancer for Employees Service

Create a Network Load Balancer

ancer for the `employees` service.

![image](https://github.com/user-attachments/assets/9d1b4dd7-5c8c-49c3-a20b-53558d789783)

### Step 6: Create Target Group for Employees Service

![image](https://github.com/user-attachments/assets/9e859e61-855b-496a-94af-078e26a4f6b4)

### Step 7: Add Health Check Path for Employees Service

![image](https://github.com/user-attachments/assets/792c08d8-c6cf-4642-b4a5-1f3a0e314686)

### Step 8: Register Target for Employees Service

![image](https://github.com/user-attachments/assets/9feb8ab3-2324-49ac-a11a-4ef1bb58af0b)

### Step 9: Add Listener for Network Load Balancer

![image](https://github.com/user-attachments/assets/4bcd5433-dd59-4030-9f65-2d53c46086a0)

**Ensure ports 5432, 8080, and 3000 are open in the security group.**

---

## Index Page for Redirecting to Microservices

### Step 1: Create an `index.html` File

Create a simple `index.html` page that provides links to each of the microservices.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Microservices</title>
</head>
<body>
    <h1><a href="<todo_load_balancer_endpoint>">To Connect Todo</a></h1>
    <h1><a href="<student_load_balancer_endpoint>">To Connect Student</a></h1>
    <h1><a href="<employees_load_balancer_endpoint>">To Connect Employees</a></h1>
</body>
</html>
```

### Step 2: Create S3 Bucket

Create an S3 bucket to host the `index.html` file.

![image](https://github.com/user-attachments/assets/d0f9e90a-f9e8-48d3-8489-d3fc87506d00)

### Step 3: Enable Static Website Hosting

Enable static web hosting and specify the `index.html` file.

![image](https://github.com/user-attachments/assets/d0d14db9-e802-485c-95bb-daebb7c615c2)

### Step 4: Set Access Control List (ACL)

Make the S3 bucket public to allow access to the `index.html`.

![image](https://github.com/user-attachments/assets/46e3057b-a1aa-4027-84dc-8e42c140bb4f)

### Step 5: Disable Block Public Access

Disable the block public access feature.

![image](https://github.com/user-attachments/assets/2f513b22-1f88-4d94-9c63-058ec6ea004e)

### Step 6: Create a Hosted Zone in Route 53

Create a hosted zone for the S3 bucket.

![image](https://github.com/user-attachments/assets/7aa4d192-e8f5-44e3-be1b-b67bdf941631)

### Step 7: Create a Record for the S3 Bucket

Create a DNS record pointing to the S3 bucket's static website endpoint.

![image](https://github.com/user-attachments/assets/c53f7e9f-88b8-4590-89ec-73fb83fe2971)

### Step 8: Test the Setup

Now, visit the URL created in Route 53 to check if it redirects to the microservices.

---

## Conclusion

You’ve successfully set up three microservices (`todo`, `student`, and `employees`) with load balancers, created an index page in S3, and set up routing through Route 53 to the various services. Your setup is now complete!

--- 

**Note:** Ensure that the correct security groups, VPC settings, and IAM roles are configured to allow all required traffic between components.
