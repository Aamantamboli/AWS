# Accessing AWS S3 with WinSCP and Cyberduck

This guide will walk you through the process of accessing your AWS S3 buckets using **WinSCP** and **Cyberduck** after creating an IAM user and configuring access credentials. Follow these steps to connect to your S3 bucket and manage your files.

## Prerequisites

- An **IAM user** in AWS with **S3 access**.
- **Access Key** and **Secret Access Key** for the IAM user.
- **WinSCP** and **Cyberduck** installed on your system.

---

## Step 1: Go to IAM and Create an IAM User

1. Open the **IAM Management Console** in AWS.
2. Click on **Users** and then **Add User**.
3. Provide a **username**, select **Programmatic access** (for access keys), and proceed.
4. Attach the appropriate policies for S3 access (e.g., `AmazonS3FullAccess`).

![image](https://github.com/user-attachments/assets/8011fe1b-27a9-4d0b-a67d-64129483be89)

---

## Step 2: Create an Access Key

1. After creating the IAM user, go to the **Users** section and select the newly created user.
2. Under the **Security credentials** tab, click **Create access key**.
3. **Download the `.csv` file** containing the **Access Key** and **Secret Access Key**. **Note**: The secret access key will only be visible once, so ensure you save it securely.

![image](https://github.com/user-attachments/assets/e8cdb501-f079-46b3-926f-75b5f5b1255f)

---

## Step 3: Log in to AWS Using the IAM Credentials

1. Open **AWS Management Console**.
2. Use the **Access Key** and **Secret Access Key** from the previous step to authenticate via the AWS CLI or other tools that require these credentials.

---

## Step 4: Create an S3 Bucket

1. Navigate to the **S3 Dashboard** in AWS.
2. Click **Create Bucket**.
3. Choose a unique name for your bucket, select the appropriate region, and configure other settings.
4. Click **Create** to finish.

![image](https://github.com/user-attachments/assets/ef35f1ac-60d5-4120-8a03-128c4e784fc1)

---

## Step 5: Download and Install WinSCP

1. Go to the **[WinSCP official website](https://winscp.net/eng/download.php)** and download the installer.
2. Install **WinSCP** on your system.

---

## Step 6: Create a New Connection in WinSCP and Select Amazon S3

1. Open **WinSCP**.
2. Click **New Session**.
3. Select **Amazon S3** from the **File Protocol** drop-down menu.
4. In the **Access Key ID** and **Secret Access Key** fields, paste the credentials you generated for your IAM user.

![image](https://github.com/user-attachments/assets/9eb2aded-10eb-4ad4-99c4-028416e46efb)

---

## Step 7: Successfully Connect with WinSCP

Once connected, you will be able to browse and manage files within your S3 bucket directly in the **WinSCP** interface.

![image](https://github.com/user-attachments/assets/36f73319-2bc8-45ee-8a53-08d8d338b8dd)

---

## Step 8: Download and Install Cyberduck

1. Go to the **[Cyberduck official website](https://cyberduck.io/download/)** and download the installer.
2. Install **Cyberduck** on your system.

---

## Step 9: Create a New Connection in Cyberduck and Select Amazon S3

1. Open **Cyberduck**.
2. Click **Open Connection**.
3. Select **Amazon S3** from the protocol list.
4. Paste your **Access Key** and **Secret Access Key** in the respective fields.

![image](https://github.com/user-attachments/assets/d9931957-1a25-4f0c-a8b4-cc7246169954)

---

## Step 10: Successfully Connect with Cyberduck

Once successfully connected, you will be able to browse and manage files within your S3 bucket.

![image](https://github.com/user-attachments/assets/dbb6cfe4-dd56-4cea-a548-4fcfaca231da)

---

## Important Notes

- **Save your credentials**: Once you create an access key, ensure you download the `.csv` file, as the **Secret Access Key** is only shown once and cannot be retrieved later.
- **IAM User Permissions**: Ensure that your IAM user has the appropriate permissions (e.g., `AmazonS3FullAccess`) to interact with S3.
- **Security**: Use these keys securely and avoid sharing them publicly.

---

## Conclusion

You have successfully connected to your AWS S3 bucket using both **WinSCP** and **Cyberduck**. You can now easily upload, download, and manage your files from your S3 bucket using these tools.

For further information, you can refer to the official documentation of **[AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/)**, **[WinSCP](https://winscp.net/eng/docs/start)**, and **[Cyberduck](https://cyberduck.io/)**.
