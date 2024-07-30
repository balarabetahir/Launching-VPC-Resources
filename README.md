# Launching-VPC-Resources
💻 Launch an EC2 instance in your public subnet. 🤐 Launch an EC2 instance in your private subnet. ⚡️ Use the Amazon VPC's wizard to create VPCs at a lightning fast pace.

Amazon Virtual Private Cloud (VPC) is a crucial component of Amazon Web Services (AWS), allowing users to provision a logically isolated section of the AWS cloud. With VPC, you can launch AWS resources into a virtual network that you define, giving you complete control over your network environment, including IP address ranges, subnets, route tables, and network gateways.

This guide will walk you through the process of launching VPC resources, focusing on security aspects. We will cover the following steps:

Launching a public EC2 instance.
Launching a private EC2 instance.
Using the VPC resource map to visualize and manage your network components.

By the end of this guide, you will have a secure and functional VPC setup with both public and private EC2 instances.

Step 1: Launch a Public EC2 Instance
1.1 Create a VPC
Before launching any EC2 instances, you need to create a VPC.
Open the VPC Dashboard in the AWS Management Console.
Click on "Create VPC".
Provide the necessary details:
Name tag: MyVPC
IPv4 CIDR block: 10.0.0.0/16
Tenancy: Default
Click "Create VPC".
1.2 Create a Public Subnet
Navigate to the Subnets section in the VPC Dashboard.
Click on "Create Subnet".
Provide the necessary details:
Name tag: PublicSubnet
VPC: Select MyVPC
Availability Zone: Select one (e.g., us-east-1a)
IPv4 CIDR block: 10.0.1.0/24
Click "Create subnet".
1.3 Create an Internet Gateway
Navigate to the Internet Gateways section.
Click on "Create internet gateway".
Provide a name tag: MyInternetGateway.
Click "Create internet gateway".
Attach the Internet Gateway to MyVPC.
1.4 Configure Route Table
Navigate to the Route Tables section.
Select the route table associated with MyVPC.
Click on "Edit routes".
Add a new route:
Destination: 0.0.0.0/0
Target: MyInternetGateway
Click "Save routes".
Associate this route table with PublicSubnet.
1.5 Launch the Public EC2 Instance
Navigate to the EC2 Dashboard and click on "Launch Instance".
Choose an Amazon Machine Image (AMI). For this guide, we'll use Amazon Linux 2.
Select an instance type (e.g., t2.micro).
Configure the instance:
Network: MyVPC
Subnet: PublicSubnet
Auto-assign Public IP: Enable
Add storage if needed.
Configure Security Group:
Create a new security group named PublicSG.
Allow SSH access from your IP (e.g., 0.0.0.0/0 for testing, but ideally your specific IP).
Review and launch the instance.
Download and save the key pair securely (e.g., MyKeyPair.pem).


Step 2: Launch a Private EC2 Instance
2.1 Create a Private Subnet
Navigate to the Subnets section in the VPC Dashboard.
Click on "Create Subnet".
Provide the necessary details:
Name tag: PrivateSubnet
VPC: Select MyVPC
Availability Zone: Select one (e.g., us-east-1a)
IPv4 CIDR block: 10.0.2.0/24
Click "Create subnet".
2.2 Configure Route Table for Private Subnet
Ensure the private subnet is using the main route table without an internet gateway route.
2.3 Launch the Private EC2 Instance
Navigate to the EC2 Dashboard and click on "Launch Instance".
Choose an AMI. For this guide, we'll use Amazon Linux 2.
Select an instance type (e.g., t2.micro).
Configure the instance:
Network: MyVPC
Subnet: PrivateSubnet
Add storage if needed.
Configure Security Group:
Create a new security group named PrivateSG.
Allow SSH access only from the PublicSubnet (e.g., 10.0.1.0/24).
Review and launch the instance.
Use the same key pair (MyKeyPair.pem) for secure access.

Step 3: Visualize and Manage VPC Resources
3.1 VPC Resource Map
AWS provides a VPC resource map that helps you visualize how different components like subnets, route tables, and internet gateways are connected.
Open the VPC Dashboard.
Navigate to the "Your VPCs" section.
Select MyVPC and click on "Actions" -> "View VPC Resource Map".
The resource map will show the relationships between your VPC components, helping you manage and troubleshoot your network setup efficiently.
Security Considerations
Key Pairs: Ensure your key pairs are stored securely. Do not share them or upload them to any source code repository.
Security Groups: Use restrictive security group rules. Only open the necessary ports and restrict access to known IP addresses.
Subnets: Keep sensitive resources in private subnets to prevent direct access from the internet.
NACLs: Network Access Control Lists (NACLs) can provide an additional layer of security by controlling inbound and outbound traffic at the subnet level.
Monitoring: Use AWS CloudWatch and VPC Flow Logs to monitor and log network traffic for security and troubleshooting purposes.

Conclusion
By following this guide, you have successfully launched and configured both public and private EC2 instances within your VPC, ensuring a secure setup. Using the VPC resource map, you can visualize and manage your network components, making it easier to maintain and scale your infrastructure. Remember, security is an ongoing process, so continuously monitor and update your configurations to protect your resources.
