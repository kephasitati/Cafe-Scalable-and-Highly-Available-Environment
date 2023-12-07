# Café Scalable and Highly Available Environment

## Module 9 - Challenge Lab: Creating a Scalable and Highly Available Environment for the Café

### Scenario
The café is set to feature in a renowned TV food show, anticipating a surge in web traffic. Sofía and Nikhil aim to make the café’s web server scalable and highly available to handle potential spikes in user traffic. This challenge lab involves implementing a robust architecture for the café's web application.

### Lab Overview and Objectives
In this lab, Elastic Load Balancing and Amazon EC2 Auto Scaling will be utilized to create a scalable and highly available environment on AWS. The objectives include:

- Inspecting a VPC
- Updating a network for multi-Availability Zone functionality
- Creating an Application Load Balancer
- Creating a launch template
- Creating an Auto Scaling group
- Testing load balancing and automatic scaling

**Note:** Step-by-step instructions are not provided for most tasks. Participants must independently complete the tasks.

### Task 2: Creating a NAT Gateway
To achieve high availability, a NAT gateway is required for the second Availability Zone. Follow these steps:

1. Create a NAT gateway in the Public Subnet of the second Availability Zone.
2. Configure the network to route internet-bound traffic from instances in Private Subnet 2 to the newly created NAT gateway.

### Task 3: Creating a Bastion Host Instance
Create a bastion host in a public subnet for future tasks. The instance should meet the following criteria:

- Name: Bastion Host
- AMI: Amazon Linux 2023 AMI
- Instance type: t2.micro
- Key pair: Vockey key pair
- Auto-assign Public IP: Enabled
- Traffic rules: Only allow SSH (Port: 22) from your IP address

### Task 4: Creating a Launch Template
Create a launch template using the AMI generated from the CafeWebAppServer instance. Specifications include:

- AMI: Cafe WebServer Image
- Instance type: t2.micro
- Key pair: New key pair (download to local computer)
- Security groups: CafeSG
- Resource tags: Name: webserver, Resource types: Instances
- IAM Instance Profile: CafeRole (Advanced Details)

### Task 5: Creating an Auto Scaling Group
Now that the launch template is defined, create an Auto Scaling group with the following criteria:

- Launch template: Use the previously created launch template
- VPC: Use the configured VPC
- Subnets: Use Private Subnet 1 and Private Subnet 2
- Group size: Desired capacity: 2, Minimum capacity: 2, Maximum capacity: 6
- Target tracking scaling policy: Metric type: Average CPU utilization, Target Value: 25, Instances need: 60

### Task 6: Creating a Load Balancer
Create an HTTP Application Load Balancer to distribute traffic across private instances:

- VPC: Use the configured VPC
- Subnets: Use two public subnets
- Security group: Create new, allowing HTTP traffic from anywhere
- Target group: Create new
- Wait until the load balancer is active, then modify the Auto Scaling group to include this load balancer.

### Task 7: Testing the Web Application
Test the café web application by visiting the DNS name of the load balancer and appending /cafe to the URL.

### Task 8: Testing Automatic Scaling under Load
Test whether the café application scales out automatically:

1. Use SSH through the bastion host to connect to a running web server instance.
2. Modify CafeSG security group to allow SSH traffic from the bastion host.
3. On the web server instance, install stress and initiate a stress test.
4. Verify that the Auto Scaling group deploys new instances during the test.

**Note:** If any issues arise during testing, review network configuration, route tables, launch template specifications, load balancer settings, instance deployment, and security group configurations.

---

By completing these tasks, Sofía ensures the café's web application is highly available and scales seamlessly to meet customer demand.
