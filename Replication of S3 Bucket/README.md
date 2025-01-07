# Create S3 Bucket in Mumbai Region and Replicate in Tokyo Region

This guide walks you through creating an S3 bucket in the Mumbai region, enabling versioning and object lock, and then setting up replication to another S3 bucket in the Tokyo region.

---

## Prerequisites

- AWS Account
- Basic knowledge of S3, AWS Console, and bucket replication
- Ensure you have appropriate permissions for creating and managing S3 buckets and IAM roles

---

## Step 1: Create S3 Bucket in Mumbai Region

1. Go to the **S3 Console** and click on **Create bucket**.
2. Choose the **Mumbai** region from the **Region** dropdown list.
3. Provide a unique **Bucket name** and configure other settings as needed.
4. Click **Create**.

![image](https://github.com/user-attachments/assets/0b5ea056-8993-4cfb-9d70-42507a3d0c1f)

---

## Step 2: Enable Bucket Versioning

1. After creating the bucket, go to the **Properties** tab of the bucket.
2. Under **Bucket Versioning**, click **Edit** and enable versioning.
3. Click **Save changes**.

![image](https://github.com/user-attachments/assets/f37e057d-a891-4254-bb83-985707b5e6b6)

---

## Step 3: Enable Object Lock

1. In the **Properties** tab of the bucket, find **Object Lock** and click **Edit**.
2. Enable **Object Locking** to protect your objects from deletion or overwriting.
3. Click **Save changes**.

![image](https://github.com/user-attachments/assets/2c905d9f-30f7-4c7c-873f-52848cf41b8e)

---

## Step 4: Create S3 Bucket in Tokyo Region

1. Follow the same process to create an S3 bucket in the **Tokyo** region.
2. Provide a unique **Bucket name** and configure other settings.
3. Click **Create**.

![image](https://github.com/user-attachments/assets/bf2e922e-1141-48ea-8518-b62d0a126048)

---

## Step 5: Enable Bucket Versioning in Tokyo Region

1. In the **Tokyo** region bucket, go to the **Properties** tab.
2. Under **Bucket Versioning**, click **Edit** and enable versioning.
3. Click **Save changes**.

![image](https://github.com/user-attachments/assets/f0217498-f389-4b0e-a24c-d43097c514d9)

---

## Step 6: Enable Object Lock in Tokyo Region

1. In the **Tokyo** region bucket, go to the **Properties** tab.
2. Enable **Object Locking** to protect objects in this bucket.
3. Click **Save changes**.

![image](https://github.com/user-attachments/assets/e7954ed3-d5db-48ea-bcb8-2d419474e24a)

---

## Step 7: Go to Management of Mumbai Bucket

1. In the **Mumbai** region, navigate to the **Management** tab of the Mumbai S3 bucket.
2. Click **Replication**.

![image](https://github.com/user-attachments/assets/0043d87c-2850-4e70-ba01-88fc233bbd6a)

---

## Step 8: Create Replication Rule

1. Click **Create replication rule**.
2. Provide a **Replication rule name** and configure replication options as needed.

![image](https://github.com/user-attachments/assets/ded9e057-77d7-44f1-8c77-560546ab9c57)

---

## Step 9: Select Objects to Replicate

1. You can choose to replicate only certain objects based on criteria such as file extensions (e.g., `.png`, `.txt`).
2. Configure this option as per your requirements.

![image](https://github.com/user-attachments/assets/ff6b547f-8efc-4b0f-89a0-967efa330714)

---

## Step 10: Replicate All Objects

1. If you want to replicate **all objects** in the bucket, select that option.

![image](https://github.com/user-attachments/assets/c0e44479-ef71-4c9e-ae82-6e8d7ad7c16f)

---

## Step 11: Replicate to Same Account

1. To replicate to a bucket in the **same AWS account**, provide the **Bucket name** for the Tokyo region bucket.

![image](https://github.com/user-attachments/assets/88eadd5f-8524-4f38-9030-9645b70a2d89)

---

## Step 12: Replicate to Another Account

1. You can also replicate to a **bucket in another AWS account**. To do this, provide the **Account ID** and **Bucket name** in the Tokyo region.

![image](https://github.com/user-attachments/assets/88de4304-48a4-4c82-9ebe-fc42780f48df)

---

## Step 13: Create a New IAM Role for Replication

1. To grant permission for replication, create a new IAM role.
2. AWS will automatically provide a policy for replication.
3. Assign the role to the replication rule.

![image](https://github.com/user-attachments/assets/42094a8b-68f2-44b4-88fb-d47a22631a5e)

---

## Step 14: Choose Whether to Replicate Existing Objects

1. Decide whether to replicate **existing objects** that are already in the Mumbai bucket.
2. Choose **Yes** if you want to replicate all objects, or **No** if you want to replicate only new objects.

![image](https://github.com/user-attachments/assets/83178a03-3423-44c1-bf3b-2891bbdcc2ce)

---

## Step 15: Provide Bucket Path and Create Role

1. Provide the **source bucket path** for the Mumbai bucket and confirm the role settings.
2. Click **Create role** to finalize the replication setup.

![image](https://github.com/user-attachments/assets/55cda5bf-f9cf-45b4-8c43-400f0901bbb6)

---

## Step 16: Object Successfully Replicated in Tokyo Region

1. After the replication rule is set up, objects from the Mumbai bucket will be automatically replicated to the Tokyo bucket.
2. Verify that the object is replicated by checking the **Tokyo** region S3 bucket.

![image](https://github.com/user-attachments/assets/2f0ca1df-2b18-4b62-ab81-0f83d215b564)

---

## Conclusion

You have successfully created an S3 bucket in the Mumbai region, enabled versioning and object lock, and set up replication to an S3 bucket in the Tokyo region.

### Important Notes:

- Replication can only be enabled for buckets with versioning enabled.
- Ensure that the IAM roles and policies have the necessary permissions to allow cross-region replication.
- Object lock ensures that the objects in your bucket cannot be deleted or overwritten for a specified retention period.

---

## References

- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/index.html)
- [S3 Bucket Replication](https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html)
- [AWS IAM Roles and Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
