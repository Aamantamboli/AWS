# Created 2-Tier Architecture in AWS

This guide demonstrates how to set up a 2-tier architecture in AWS using **EC2** for hosting the application and **RDS** for the database service.

---

## Step 1: Create RDS (Relational Database Service)

1. Go to the **RDS Dashboard** in AWS.
2. Select **Create Database** and choose **MySQL** (or your preferred database engine).
3. Choose **Free tier** (if eligible) and configure your database instance.
4. Under **Settings**, provide a **DB Instance Identifier**, **Master Username**, and **Master Password**.
5. Set **Public accessibility** to **Yes** for external connections.

![Screenshot 2024-08-15 114918](https://github.com/user-attachments/assets/39febed4-d50a-47b2-8bed-81ef16a54bbf)

---

## Step 2: Create a New Password and Select Public Access

1. Once RDS is created, go to the **Configuration** section.
2. Copy the **Endpoint** and note it down for future use.
3. Select **Public Accessibility** as **Yes** (to allow connections from your EC2 instance).

![Screenshot 2024-08-15 115008](https://github.com/user-attachments/assets/a8a04705-1bf3-4f1e-8622-0d9e0dbbac0a)

---

## Step 3: Launch EC2 Instance

1. Go to the **EC2 Dashboard** in AWS.
2. Click on **Launch Instance** and configure it according to your needs.
3. Make sure to configure **Security Groups** to allow the following ports:
    - **SSH (port 22)** for remote access.
    - **HTTP (port 80)** for web access.
    - **HTTPS (port 443)** for secure web access.
    - **TCP (port 3306)** for database access.

![Screenshot 2024-08-15 115022](https://github.com/user-attachments/assets/eff714ab-3f86-45a4-8e43-dbb64db62eed)

---

## Step 4: Copy Public IP and Connect via MobaXterm

1. After launching your EC2 instance, copy its **Public IP**.
2. Open **MobaXterm** or any SSH client and paste the public IP.
3. Select your private key to authenticate the connection.

![Screenshot 2024-08-12 215819](https://github.com/user-attachments/assets/f3b48a39-002a-45eb-a8da-3550a691cbd3)

---

## Step 5: Connect to EC2 Instance and Upload Your `.war` and `.jar` Files

Once connected to your EC2 instance, follow these commands:

1. Download and extract Apache Tomcat:
   
   ```bash
   curl -O https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz
   tar -xvf apache-tomcat-9.0.93.tar.gz
   sudo mv apache-tomcat-9.0.93 /opt/
   ```

2. Upload the `.war` (application) and `.jar` (MySQL connector) files to the Tomcat webapps and lib directories:

   ```bash
   sudo mv student.war /opt/apache-tomcat-9.0.93/webapps/
   sudo mv mysql-connector.jar /opt/apache-tomcat-9.0.93/lib/
   ```

3. Install Java 1.8:

   ```bash
   sudo yum install java-1.8.0-amazon-corretto-devel.x86_64 -y
   ```

4. Change the directory to Tomcat’s location:

   ```bash
   cd /opt/apache-tomcat-9.0.93/
   ```

5. Edit the `context.xml` file to configure database connection:

   ```bash
   vim conf/context.xml
   ```

---

## Step 6: Edit the `context.xml` File with Database Credentials

Edit the `context.xml` file in the Tomcat configuration directory (`/opt/apache-tomcat-9.0.93/conf/`) and replace the placeholders with your database details.

```xml
<Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
          maxTotal="100" maxIdle="30" maxWaitMillis="10000"
          username="<username>" password="<password>" driverClassName="com.mysql.jdbc.Driver"
          url="jdbc:mysql://<database_endpoint>:3306/<db_name>"/>
```

- Replace `<username>` with your database username.
- Replace `<password>` with your database password.
- Replace `<database_endpoint>` with the RDS endpoint you copied earlier.
- Replace `<db_name>` with the name of your database (e.g., `students`).

---

## Step 7: Install MariaDB on EC2 Instance

1. Install MariaDB on the EC2 instance (for database operations):

   ```bash
   sudo yum install mariadb105.x86_64 -y
   ```

2. Connect to the RDS database:

   ```bash
   mysql -h <database_endpoint> -u <username> -p<password>
   ```

3. Create a database and required table:

   ```sql
   CREATE DATABASE <db_name>;
   USE <db_name>;

   CREATE TABLE IF NOT EXISTS students(
       student_id INT NOT NULL AUTO_INCREMENT,
       student_name VARCHAR(100) NOT NULL,
       student_addr VARCHAR(100) NOT NULL,
       student_age VARCHAR(3) NOT NULL,
       student_qual VARCHAR(20) NOT NULL,
       student_percent VARCHAR(10) NOT NULL,
       student_year_passed VARCHAR(10) NOT NULL,
       PRIMARY KEY (student_id)
   );
   ```

4. Exit the MySQL session:

   ```bash
   exit
   ```

5. Start Tomcat to deploy your `.war` file:

   ```bash
   bash bin/catalina.sh start
   ```

---

## Summary

1. **RDS** (Relational Database Service) is created and configured for public access.
2. **EC2 instance** is set up and configured with necessary ports.
3. **Tomcat** is installed on the EC2 instance, and the `.war` and `.jar` files are uploaded.
4. **Database connection details** are configured in Tomcat’s `context.xml` file.
5. **MariaDB** is installed, and the necessary database and table for the application are created.
6. **Tomcat** is started to run the application.

Now, you can access your application by using the EC2 public IP and the appropriate port (usually 8080 for Tomcat). 
