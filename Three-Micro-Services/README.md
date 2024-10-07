<h1>HOSTED THREEE MICRO SERVICE TODO, STUDENT AND EMPLOYEES REDIRECT IT IN INDEX PAGE</h1>
<h2>1st MICRO SERVICE</h2>
<h3>Step 1: Create Instance </h3>

![image](https://github.com/user-attachments/assets/6a446752-4e60-4faf-a1d8-fe0cade2f3f7)

<h3>Step 2: Connect Instance</h3>

```
sudo yum install httpd -y
sudo yum install git -y
git clone https://github.com/Aamantamboli/application.git
sudo mv application/todo/ /var/www/html/
sudo systemctl enable httpd
sudo systemctl start httpd
```

<h3>Step 3: Create Application Load Balancer for 1st Micro Service</h3>

![image](https://github.com/user-attachments/assets/194ec6ad-2899-465e-90e2-1c17de6184dd)

<h3>Step 5: Create Target Group</h3>

![image](https://github.com/user-attachments/assets/76ad9ed5-a2ca-4d24-8e3e-c0799e6f112c)

<h3>Step 5: Give Health Check Path</h3>

![image](https://github.com/user-attachments/assets/6e49dc9a-5b73-4b31-88be-2007e0c9f7b6)

<h3>Step 6: Register Target</h3>

![image](https://github.com/user-attachments/assets/b593f608-8cea-4284-8ce2-06677a8aaae6)

<h3>Step 7: Add Listener in Load Balancer</h3>

![image](https://github.com/user-attachments/assets/e393f20b-141e-45af-a4bc-dd5742e8f67c)

<h2>2nd MICRO SERVICE</h2>
<h3>Step 1: Create RDS (Relational Database Service) and select MariaDB</h3>

![image](https://github.com/user-attachments/assets/6665600a-d8be-4ea7-afd2-1d243af32b56)

<h3>Step 2: Select free tier and create a new password </h3>

![image](https://github.com/user-attachments/assets/68a0f003-3ff8-478f-9a85-6df3bf3d65b2)

![image](https://github.com/user-attachments/assets/aaed2d38-cc84-47c5-ba4a-a59207d23f6d)

<h3>Step 3: Create Instance and Connect it </h3>

```
curl -O https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz
tar -xvf apache-tomcat-9.0.93.tar.gz
sudo mv apache-tomcat-9.0.93 /opt/
sudo mv student.war /opt/apache-tomcat-9.0.93/webapps/
sudo mv mysql-connector.jar /opt/apache-tomcat-9.0.93/lib/
sudo yum install java-1.8.0-amazon-corretto-devel.x86_64 -y
cd /opt/apache-tomcat-9.0.93/
vim conf/context.xml
```

<h3>Step 4: Edit this in conf/context.xml your username, your password and endpoint of database and database name</h3>

```
<Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
               maxTotal="100" maxIdle="30" maxWaitMillis="10000"
               username="<username>" password="<password>" driverClassName="com.mysql.jdbc.Driver"
               url="jdbc:mysql://<database_enpoint>:3306/<db_name>"/>
```

<h3>Step 5: Install Mariadb</h3>

```
sudo yum install  mariadb105.x86_64 -y

mysql -h <database_endpoint> -u <username> -p<password>

create database <db_name>;

use <db_name>;

CREATE TABLE if not exists students(student_id INT NOT NULL AUTO_INCREMENT,
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

<h3>Step 5: Create Application Load Balancer for 2nd Micro Service</h3>

![image](https://github.com/user-attachments/assets/3b3d0e45-2d5d-4981-8bf0-8a35aa3b3578)

<h3>Step 6: Create Target Group</h3>

![image](https://github.com/user-attachments/assets/e6c6a40b-90fa-4408-91f0-83ba137f1d2b)

<h3>Step 7: Give Health Check Path</h3>

![image](https://github.com/user-attachments/assets/ec7cb748-13ab-40dd-9e3a-03a1b3b188e5)

<h3>Step 8: Register Target</h3>

![image](https://github.com/user-attachments/assets/67fdb6e7-d16e-4def-9d44-946db13c0548)

<h3>Step 9: Add Listener in Load Balancer</h3>

![image](https://github.com/user-attachments/assets/831fcd53-fc30-4efb-9323-9e453a187ebe)

**Must have TCP 8080 Port in Security group**

<h2>3rd MICRO SERVICE</h2>
<h3>Step 1: Launch one Instance for Frontend</h3>

![image](https://github.com/user-attachments/assets/2c43de5a-5fa2-4f04-acef-34bdc317bf74)

<h3>Step 2: Launch another Instance for Backend and PostgreSQL</h3>

![image](https://github.com/user-attachments/assets/ea17ff76-ad94-4c65-af68-6c7e1863da33)

<h3>Step 3: Connect Frontend Instance </h3>

```
sudo apt update
sudo apt install -y nodejs npm
sudo npm install -g n
sudo n 14.17.0 node -v0
sudo apt-get install git-all -y
git clone https://github.com/shubhamkalsait/devops-fullstack-app.git
cd devops-fullstack-app/frontend/
sudo vim .env 	REACT_APP_SERVER_URL=http://backend_pub_ip:8080/employees
npm install
npm start
```

<h3>Step 4: Connect Backend and PostgreSQL Instance</h3>

```
sudo apt update
sudo apt install postgresql postgresql-contrib -y<br>
sudo passwd postgres
sudo -u postgres psql
CREATE DATABASE db_name; #employees
CREATE USER user_name WITH PASSWORD 'password'; #test #'1234'
GRANT ALL PRIVILEGES ON DATABASE db_name TO user_name; #employees #test
\c your_db_name
GRANT USAGE ON SCHEMA public TO your_user;
GRANT ALL PRIVILEGES ON SCHEMA public TO your_user;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO your_user;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL ON TABLES TO your_user;
\q
exit
sudo curl -O https://dl.google.com/go/go1.19.linux-amd64.tar.gz
sudo tar -xvf go1.19.linux-amd64.tar.gz
sudo mv go /usr/local
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
sudo snap install go --classic
sudo apt-get install git-all -y
git clone https://github.com/shubhamkalsait/devops-fullstack-app.git
cd devops-fullstack-app/backend/
sudo DB_HOST=localhost DB_USER=<your_username> DB_PASSWORD=<your_password> DB_NAME=<your_dbname> DB_PORT=5432 ALLOWED_ORIGINS="http://frontend_pub_ip:3000" go run main.go
```

<h3>Step 5: Create Network Load Balancer for 3rd Micro Service </h3>
  
![image](https://github.com/user-attachments/assets/f041d0a4-1db4-4253-a996-9757e70d6485)

<h3>Step 6: Create Target Group</h3>

![image](https://github.com/user-attachments/assets/8a05e870-c9d2-469d-a9d5-a5359e5b61f5)

<h3>Step 7: Give Health Check Path</h3>

![image](https://github.com/user-attachments/assets/85bbdb75-5ea2-4b6b-af0a-4a6a0d5fc8fb)

<h3>Step 8: Register Target</h3>

![image](https://github.com/user-attachments/assets/d039f605-39bc-4314-9414-c64517d7723e)

<h3>Step 9: Add Listener in Load Balancer</h3>

![image](https://github.com/user-attachments/assets/ebd7aee4-910b-4fb2-b53c-8dacde9d2bc9)

**Must have 5432,8080,3000 port in Security Group**

<h2>INDEX PAGE</h2>
<h3>Step 1: Create new file of index.html and add all micro services load balancer endpoint in it under &lt;a&gt;tag</h3>

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mcro Services</title>
</head>
<body>
    <h1><a href="<load_balancer_endpoint>">To Connect todo</a>T</h1>
        <h1><a href="<load_balancer_endpoint>"></a>To Connect student</h1>
            <h1><a href="<load_balancer_endpoint>"></a>To Connect employees</h1>
</body>
</html>
```

<h3>Step 2: Create a S3 bucket</h3>

![image](https://github.com/user-attachments/assets/9017ebfd-c938-4842-8ed8-fe28c9bf4f1a)

<h3>Step 3: Enable static web hosting and give default page index.html</h3>

![image](https://github.com/user-attachments/assets/ed900afc-709e-4576-98cd-9d7f5acf7d61)

<h3>Step 4: Give ACL(Access Control List)</h3>

![image](https://github.com/user-attachments/assets/0f326739-5453-4ec5-b509-8a51f9056559)

<h3>Step 5: Block public access make it off</h3>

![image](https://github.com/user-attachments/assets/d28d1fa5-00a4-4898-987a-0bb5d6afe78c)

<h3>Step 6: Create a hosted zone in route 53</h3>

![image](https://github.com/user-attachments/assets/a5525409-ec7e-4437-9057-925cba508b82)

<h3>Step 7: Create a record in it </h3>

![image](https://github.com/user-attachments/assets/5471639b-dcf3-4ba8-916b-d1f696e7f0d8)

<h3>Step 8: In record name give your bucket name make it alias and then route traffic to s3 website endpoint select your region and endpoint of bucket</h3>

![image](https://github.com/user-attachments/assets/3043f5db-238c-499a-8084-7cda39815a5b)

<h3>Step 9: Now just hit your record name </h3>

![image](https://github.com/user-attachments/assets/7c4d345c-0be3-4b68-8380-5b4b76bdea91)

<h3>Step 10: If you click on To Connect todo it will take you to todo page</h3>

![image](https://github.com/user-attachments/assets/6f0c896c-8478-4e18-8521-53f1707f86a5)

<h3>Step 11: If you click on To Connect student it will take you to student page</h3>

![image](https://github.com/user-attachments/assets/11149ccb-ab71-4b68-94d0-38d370edfb94)

<h3>Step 12: If you click on To Connect employees it will take you to employees page</h3>

![image](https://github.com/user-attachments/assets/15f71c02-1f6a-4d4e-8252-8b42d5596d95)

**Successfully hosted micro services**
