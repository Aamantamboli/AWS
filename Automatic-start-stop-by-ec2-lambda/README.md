# Stop and Start EC2 Instance Using Lambda Function

This guide explains how to stop and start an EC2 instance automatically using AWS Lambda functions and Amazon EventBridge rules. We will create Lambda functions to control EC2 instances and use EventBridge to schedule these functions.

## Prerequisites

- An AWS account
- Basic knowledge of AWS Lambda, IAM, EC2, and EventBridge
- An EC2 instance running

---

## Step 1: Create IAM Policy for Lambda to Access EC2

1. **Navigate to IAM > Policies** in the AWS Management Console.
2. Click **Create Policy**.
3. Choose the **JSON** tab and paste the following policy to allow stopping and starting EC2 instances:

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "ec2:StartInstances",
                   "ec2:StopInstances"
               ],
               "Resource": "*"
           }
       ]
   }
   ```

4. Click **Review Policy**.
5. Name the policy (e.g., `EC2-Stop-Start-Policy`) and click **Create Policy**.

---

## Step 2: Create IAM Role for Lambda

1. Go to **IAM > Roles** and click **Create Role**.
2. Select **Lambda** as the trusted entity.
3. Attach the policy you created earlier (`EC2-Stop-Start-Policy`).
4. Name the role (e.g., `Lambda-EC2-Role`) and click **Create Role**.

---

## Step 3: Create EC2 Instance

1. Navigate to the **EC2 Dashboard**.
2. Launch a new EC2 instance or use an existing one that you want to stop and start using Lambda.

---

## Step 4: Create Lambda Function to Stop EC2 Instance

1. Go to the **Lambda Console** and click **Create Function**.
2. Choose **Author from scratch** and name the function (e.g., `Stop-EC2-Instance`).
3. Choose **Python 3.x** as the runtime.
4. Select the **Execution role** as the role created earlier (`Lambda-EC2-Role`).
5. In the function code, paste the following Python code to stop the EC2 instance:

   ```python
   import boto3

   ec2 = boto3.client('ec2')

   def lambda_handler(event, context):
       response = ec2.stop_instances(
           InstanceIds=['i-xxxxxxxxxxxxxxxxx']  # Replace with your instance ID
       )
       return response
   ```

6. Click **Deploy** to save and deploy the function.

---

## Step 5: Test the Lambda Function to Stop EC2 Instance

1. In the Lambda function dashboard, click on **Test**.
2. Create a test event with the default settings and click **Test**.
3. Verify that the EC2 instance stops successfully.

---

## Step 6: Create EventBridge Rule to Trigger Lambda Function

1. Go to **Amazon EventBridge > Rules** and click **Create Rule**.
2. Set a **Cron expression** for the schedule (e.g., stop the instance at 10:00 PM UTC every day: `cron(0 22 * * ? *)`).
3. Set the **Target** as the Lambda function you created (`Stop-EC2-Instance`).
4. Click **Create Rule**.

---

## Step 7: Verify Instance Stopped at Scheduled Time

The EC2 instance should stop at the scheduled time as defined in the EventBridge rule. You can verify this by checking the EC2 console or the instance state.

---

## Step 8: Create Lambda Function to Start EC2 Instance

1. Go to the **Lambda Console** and click **Create Function**.
2. Choose **Author from scratch** and name the function (e.g., `Start-EC2-Instance`).
3. Choose **Python 3.x** as the runtime.
4. Select the **Execution role** as the role created earlier (`Lambda-EC2-Role`).
5. In the function code, paste the following Python code to start the EC2 instance:

   ```python
   import boto3

   ec2 = boto3.client('ec2')

   def lambda_handler(event, context):
       response = ec2.start_instances(
           InstanceIds=['i-xxxxxxxxxxxxxxxxx']  # Replace with your instance ID
       )
       return response
   ```

6. Click **Deploy** to save and deploy the function.

---

## Step 9: Test the Lambda Function to Start EC2 Instance

1. In the Lambda function dashboard, click on **Test**.
2. Create a test event with the default settings and click **Test**.
3. Verify that the EC2 instance starts successfully.

---

## Step 10: Create EventBridge Rule to Start EC2 Instance

1. Go to **Amazon EventBridge > Rules** and click **Create Rule**.
2. Set a **Cron expression** for the schedule (e.g., start the instance at 7:00 AM UTC every day: `cron(0 7 * * ? *)`).
3. Set the **Target** as the Lambda function you created (`Start-EC2-Instance`).
4. Click **Create Rule**.

---

## Step 11: Verify Instance Started at Scheduled Time

The EC2 instance should start at the scheduled time as defined in the EventBridge rule. You can verify this by checking the EC2 console or the instance state.

---

## Conclusion

You have successfully set up an automation system using AWS Lambda and EventBridge to stop and start EC2 instances at scheduled times. The Lambda functions interact with EC2, and EventBridge triggers them at the specified cron schedule.

---

### References

- [AWS Lambda](https://aws.amazon.com/lambda/)
- [Amazon EventBridge](https://aws.amazon.com/eventbridge/)
- [IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
- [EC2 Instances](https://aws.amazon.com/ec2/)

```
