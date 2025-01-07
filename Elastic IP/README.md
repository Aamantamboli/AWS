# Creating an Elastic IP in AWS

This guide will walk you through the process of creating and associating an **Elastic IP (EIP)** in **AWS**. Elastic IP addresses are static IP addresses designed for dynamic cloud computing. These can be associated with your EC2 instances to provide a fixed public IP address for your resources.

## Prerequisites

- An **AWS account** with access to EC2 and VPC.
- A **running EC2 instance** that you want to associate the Elastic IP with.

---

## Step 1: Log in to the AWS Management Console

1. Open your preferred browser and go to the [AWS Management Console](https://aws.amazon.com/console/).
2. Sign in using your AWS credentials.

---

## Step 2: Navigate to the EC2 Dashboard

1. In the **AWS Management Console**, type **EC2** in the search bar and select **EC2** from the services dropdown.
2. You will be directed to the **EC2 Dashboard**.

---

## Step 3: Go to the Elastic IP Section

1. In the **left sidebar** of the EC2 Dashboard, scroll down to the **Network & Security** section.
2. Click on **Elastic IPs**.

---

## Step 4: Allocate a New Elastic IP Address

1. Click on the **Allocate new address** button at the top of the Elastic IPs page.
2. In the **Allocate Elastic IP address** dialog, choose the appropriate **Scope**:
   - **VPC** (Virtual Private Cloud) is recommended for most scenarios.
3. Click the **Allocate** button to allocate a new Elastic IP address.
4. Once the EIP is allocated, you will see it listed in your **Elastic IPs** section.

---

## Step 5: Associate the Elastic IP with an EC2 Instance

1. After allocating the Elastic IP, select the new Elastic IP from the list of available IP addresses.
2. Click on the **Actions** dropdown and select **Associate Elastic IP address**.
3. In the **Associate Elastic IP address** dialog:
   - Choose the **Instance** from the dropdown list (select the EC2 instance you want to associate the Elastic IP with).
   - Optionally, choose the **Private IP address** (if the instance has multiple private IPs).
4. Click **Associate** to complete the association.

---

## Step 6: Verify the Association

1. Once associated, go back to your EC2 instance's **Description** tab.
2. Under the **Public IP** section, you should now see the Elastic IP address associated with your EC2 instance.

---

## Step 7: (Optional) Test the Elastic IP

1. If you associated the Elastic IP with an EC2 instance running a web server, you should now be able to access your instance using the new Elastic IP address from a browser.
2. For SSH access, you can use the following command:
   
   ```bash
   ssh -i /path/to/your-key.pem ec2-user@<Elastic-IP>
   ```

   Replace `<Elastic-IP>` with the Elastic IP address assigned to your EC2 instance.

---

## Step 8: Release the Elastic IP (If Not Needed)

1. If you no longer need the Elastic IP, you can release it to avoid additional charges.
2. In the **Elastic IPs** section, select the IP address you wish to release.
3. Click on **Actions** and then **Release Elastic IP address**.

**Important Note:** You will incur charges for Elastic IP addresses that are not associated with a running EC2 instance.

---

## Important Considerations

- **Elastic IP Costs**: Elastic IP addresses are free as long as they are associated with a running EC2 instance. However, if the Elastic IP is not associated with an instance or if it's associated with a stopped instance, AWS will charge you a small fee.
  
- **Limitations**: AWS accounts have a default limit of **5 Elastic IPs per region**. If you need more, you can request an increase through the [AWS Support Center](https://console.aws.amazon.com/support/home).

- **Public IPs vs Elastic IPs**: An Elastic IP is a static, public IPv4 address designed for dynamic cloud computing. If you stop an EC2 instance that is using a public IP, that IP will be released. However, with an Elastic IP, you retain the same IP even after the instance is stopped or restarted.

---

## Conclusion

You have successfully created an Elastic IP (EIP) and associated it with your EC2 instance. This allows your EC2 instance to maintain a static public IP, ensuring consistent access even when instances are restarted or stopped.

For further information on managing Elastic IPs, refer to the [AWS Elastic IP Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses.html).
