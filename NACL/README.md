# Creating and Configuring a Network Access Control List (NACL) in AWS

A **Network Access Control List (NACL)** in AWS is a stateless firewall that controls traffic moving in and out of a subnet in your **VPC**. It provides an additional layer of security by allowing or denying traffic based on IP addresses, protocols, and ports. In this guide, we will walk through the process of creating and configuring a NACL in AWS.

## Prerequisites

- An **AWS account** with appropriate permissions to manage **VPC** and **NACL** resources.
- A **VPC** created with at least one **subnet** where you want to apply the NACL.
- Basic understanding of **CIDR blocks** and network security.

---

## Step 1: Log in to the AWS Management Console

1. Open your preferred browser and go to the [AWS Management Console](https://aws.amazon.com/console/).
2. Sign in using your AWS credentials.

---

## Step 2: Navigate to the VPC Dashboard

1. In the **AWS Management Console**, type **VPC** in the search bar and select **VPC** from the services dropdown.
2. You will be directed to the **VPC Dashboard**.

---

## Step 3: Go to the NACL Section

1. In the **VPC Dashboard**, scroll down the left sidebar to the **Network ACLs** section.
2. Click on **Network ACLs** to view and manage your NACLs.

---

## Step 4: Create a New NACL

1. Click the **Create Network ACL** button at the top of the Network ACLs page.
2. In the **Create Network ACL** dialog, you need to:
   - **Name**: Provide a name for your NACL (e.g., `MyCustomNACL`).
   - **VPC**: Select the **VPC** where you want to create the NACL.
   
   Once filled out, click **Create**.

---

## Step 5: Add Inbound and Outbound Rules to the NACL

By default, a newly created NACL comes with default rules that allow all inbound and outbound traffic. However, you can customize these rules to restrict or allow specific traffic.

### Add Inbound Rules

1. Select the newly created NACL from the list.
2. In the **Inbound Rules** tab, click on the **Edit Inbound Rules** button.
3. To add a new rule, click **Add Rule**. Enter the following details:
   - **Rule #**: Specify the rule number (e.g., `100`).
   - **Type**: Select the type of traffic to allow (e.g., **HTTP** or **SSH**).
   - **Protocol**: Select the protocol (e.g., TCP, UDP).
   - **Port Range**: Specify the port range (e.g., `80` for HTTP).
   - **Source**: Define the source IP range (e.g., `0.0.0.0/0` for all IPs).
   - **Allow/Deny**: Choose whether to **Allow** or **Deny** traffic.

   After configuring the rule, click **Save changes**.

### Add Outbound Rules

1. Switch to the **Outbound Rules** tab.
2. Click on **Edit Outbound Rules**.
3. Similarly to inbound rules, click **Add Rule**, then specify:
   - **Rule #**: Rule number (e.g., `100`).
   - **Type**: Select traffic type (e.g., **HTTP**).
   - **Protocol**: Select TCP or UDP.
   - **Port Range**: Set the port range (e.g., `80` for HTTP).
   - **Destination**: Define the destination IP range (e.g., `0.0.0.0/0` for all destinations).
   - **Allow/Deny**: Choose whether to **Allow** or **Deny** traffic.

   Once done, click **Save changes**.

---

## Step 6: Associate the NACL with a Subnet

1. After configuring your NACL, you need to associate it with a **subnet** in your VPC.
2. In the **Network ACLs** section, select the NACL you just created.
3. In the **Subnet Associations** tab, click **Edit subnet associations**.
4. Select the subnets you want to associate with the NACL by checking the boxes next to the subnet names.
5. Click **Save** to complete the association.

---

## Step 7: Verify NACL Configuration

1. Go to the **EC2 Dashboard** and launch an EC2 instance in the subnet that is associated with the NACL.
2. Try accessing the EC2 instance from a client or browser using the configured rules (e.g., try accessing HTTP port 80 if you allowed HTTP).
3. If your NACL rules are set up correctly, the traffic should be allowed or denied based on the rules.

---

## Step 8: (Optional) Modify NACL Rules

If you need to modify the rules later, simply go back to the **Network ACLs** section in the **VPC Dashboard** and:
1. Select the NACL.
2. Modify the inbound and outbound rules by clicking the **Edit** button.
3. After making changes, click **Save changes**.

---

## Important Notes

- **Stateless Nature**: NACLs are stateless, meaning you need to define rules for both inbound and outbound traffic separately. For example, if you allow inbound HTTP (port 80), you must also allow outbound traffic on port 80 for the response.
  
- **Default NACL**: Every VPC comes with a default NACL, which allows all inbound and outbound traffic. If you create a custom NACL, it will be associated with no subnets by default, and you must explicitly associate it with the subnets you wish to apply it to.

- **NACL Rule Numbers**: Rule numbers determine the order in which the rules are evaluated. Lower numbered rules are evaluated first. AWS evaluates rules in order and stops at the first match.

---

## Conclusion

You have successfully created and configured a Network Access Control List (NACL) in AWS to control the inbound and outbound traffic to your VPC subnets. NACLs add an extra layer of security by allowing you to control access based on IP address ranges, protocols, and ports.

For more details, you can refer to the [AWS NACL Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html).
