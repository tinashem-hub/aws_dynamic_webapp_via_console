# aws_dynamic_webapp_via_console
Deploying a dynamic webapp on AWS via the console.

Sure! Here's an alignment of the steps with the AWS 3-tier setup:

1. Create a VPC with the CIDR block 10.0.0.0/16.
2. Enable DNS hostname resolution for the VPC.
3. Create a Dev Internet Gateway and attach it to the Dev VPC.
4. Create public and private subnets within the VPC:
   - Public subnets: For the load balancer and web server instances.
   - Private subnets: For application servers and database instances.
5. Enable auto-assign public IP addresses for the public subnets.
6. Create a public route table and add a route to the internet via the Dev Internet Gateway.
7. Associate the two public subnets with the public route table.
8. Create the private subnet, which is associated with the main route table by default.
9. Create two NAT Gateways in the two public subnets:
   - Each NAT Gateway provides internet access for resources in the private subnets.
10. Create two routing tables, each associated with a NAT Gateway, and associate them with the subnets:
    - Public route table: Associated with the public subnets and routes traffic to the internet via the Dev Internet Gateway.
    - Private route table: Associated with the private subnets and routes traffic to the NAT Gateway.
11. Create the following security groups:
    - ALB security group: Allow port 80 and 443 from 0.0.0.0/0.
    - SSH security group: Allow port 22 from your IP.
    - Web Server security group: Allow port 80 and 443 from the ALB security group, allow port 22 from the SSH security group, and allow port 3306 for MySQL from the Web Server Security Group.
    - Database security group: Allow port 3306 for MySQL from the Web Server Security Group.

These steps align with the AWS 3-tier architecture, where the public subnets contain load balancers and web server instances, the private subnets house application servers and database instances, and the NAT Gateways provide internet access for resources in the private subnets.
