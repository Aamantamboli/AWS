<h1>STATIC WEB HOSTING</h1>
<h3>Step 1: Create instance and connect it</h3>

![image](https://github.com/user-attachments/assets/1b3f0bef-d5ae-45c1-ad61-9a41029d4724)

<h3>Step 2: Go to root user</h3>

```
sudo -i
```

<h3>Step 3: Download static website and unzip it</h3>

```
curl -O https://www.free-css.com/assets/files/free-css-templates/download/page296/oxer.zip
unzip filename
```

<h3>Step 4: Install Nginx</h3>

```
yum install nginx -y
systemctl status nginx
systemctl start nginx
systemctl restart nginx
```

<h3>Step 5: Move unzip file to nginx path</h3>

```
mv /usr/share/nginx/html
```

<h3>Step 6: Click on IP of instance and hit it on your browser </h3>

![image](https://github.com/user-attachments/assets/dafb7c14-9f1e-4ca1-8b05-817582f556ee)


**Must have (SSH,HTTP) port in security group**
