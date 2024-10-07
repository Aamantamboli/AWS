<h1>Created 2-tier Architecture in AWS</h1>

<h3>Step 1: Create RDS (Relational Database Service) </h3>

![image](https://github.com/user-attachments/assets/a3d13bf3-3ee0-4a80-b394-12da2e753790)

<h3>Step 2: Create a new password and select public access</h3>

![image](https://github.com/user-attachments/assets/94d635b0-6b72-4f3e-b6c7-1c999f569a84)

<h3>Step 3: Launch EC2 instance must have (SSH,HTTP,HTTPS,TCP) port</h3>

![image](https://github.com/user-attachments/assets/b96b6d46-0334-4146-8e9a-ab5c69371109)

<h3>Step 4: Copy public IP and paste in MobaXterm and select your key</h3>

![image](https://github.com/user-attachments/assets/d6564726-0fe5-4890-b670-cea042e5fae8)

<h3>Step5: Connect Instance and upload your .war and .jar file</h3>

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

<h3>Step 6: Edit this in conf/context.xml your username, your password and endpoint of database and database name</h3>

```
<Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
               maxTotal="100" maxIdle="30" maxWaitMillis="10000"
               username="<username>" password="<password>" driverClassName="com.mysql.jdbc.Driver"
               url="jdbc:mysql://<database_enpoint>:3306/<db_name>"/>
```

<h3>Step 7: Install Mariadb</h3>

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
