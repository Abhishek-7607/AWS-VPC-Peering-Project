# AWS-VPC-Peering-Project
AWS VPC Peering project demonstrating private communication between two VPCs.


# AWS VPC Peering Project

## 1. Project Overview

This project demonstrates how to establish private network communication between two Amazon Virtual Private Clouds (VPCs) using AWS VPC Peering.

The project was implemented using Amazon VPC, subnets, route tables, security groups, and Amazon EC2 instances.

## 2. Project Objectives

- Create two separate VPCs in AWS.
- Configure public and private subnets.
- Establish a VPC Peering connection.
- Configure route tables for communication between VPCs.
- Apply security group rules to control network traffic.
- Test private connectivity using the ping command.
- Verify how security rules affect network communication.

## 3. AWS Services Used

- Amazon VPC
- VPC Peering
- Amazon EC2
- Route Tables
- Internet Gateway
- Security Groups
- Amazon Linux 2023

## 4. Network Architecture

The project consists of two VPCs connected through a VPC Peering connection.

### VPC A

- Name: ewb-vpc-a
- CIDR Block: 10.10.0.0/16
- Public Subnet: ewb-a-public
- Public Subnet CIDR: 10.10.1.0/24
- Private Subnet: ewb-a-private
- Private Subnet CIDR: 10.10.2.0/24

### VPC B

- Name: ewb-vpc-b
- CIDR Block: 10.20.0.0/16
- Private Subnet: ewb-b-private
- Private Subnet CIDR: 10.20.1.0/24

## 5. EC2 Instances

| Instance | Private IP Address | Purpose |
|---|---|---|
| ewb-bastion | 10.10.1.10 | Secure access to private instances |
| ewb-app-a | 10.10.2.10 | Application instance in VPC A |
| ewb-app-b | 10.20.1.10 | Application instance in VPC B |

The instances use Amazon Linux 2023. The application instances do not require public IPv4 addresses for communication across the peered VPCs.

## 6. VPC Peering Configuration

1. Created VPC A and VPC B with non-overlapping CIDR blocks.
2. Created the required subnets.
3. Created and attached an Internet Gateway to VPC A.
4. Created the VPC Peering connection between VPC A and VPC B.
5. Accepted the peering request.
6. Added the required routes to the route tables.
7. Configured security groups to allow the required SSH and ICMP traffic.

## 7. Routing Configuration

### VPC A Private Route Table

- Destination: 10.10.0.0/16 — Local
- Destination: 10.20.0.0/16 — VPC Peering connection

### VPC B Private Route Table

- Destination: 10.20.0.0/16 — Local
- Destination: 10.10.0.0/16 — VPC Peering connection

The public route table in VPC A also contains a route to the Internet Gateway and a route to VPC B through the peering connection.

## 8. Security Configuration

Security groups were configured to control access to the EC2 instances.

- SSH access was restricted to the required source IP addresses.
- ICMP traffic was allowed between the two application instances for connectivity testing.
- Default outbound rules were retained.

## 9. Connectivity Testing

The ping command was used to test private communication between the application instances.

### Test 1: VPC A to VPC B

Command:

`ping -c 4 10.20.1.10`

Result: Successful. Four packets were transmitted and four were received, with 0% packet loss.

### Test 2: VPC B to VPC A

Command:

`ping -c 4 10.10.2.10`

Result: Successful. Four packets were transmitted and four were received, with 0% packet loss.

### Test 3: Security Rule Verification

The inbound ICMP rule on the App-B security group was temporarily removed.

Result: The ping test failed with 100% packet loss.

### Test 4: Connectivity Restored

The ICMP rule was restored and the ping test was repeated.

Result: Communication succeeded again with 0% packet loss.

## 10. Screenshots and Evidence

Screenshots of the AWS configuration and connectivity tests are included in this repository.

They provide evidence of the VPC configuration, subnets, peering connection, route tables, security groups, EC2 instances, and connectivity test results.

## 11. Conclusion

The AWS VPC Peering project was successfully implemented and tested.

Both application instances communicated using their private IP addresses through the VPC Peering connection. The bidirectional ping tests were successful. The controlled security test demonstrated that removing the required ICMP inbound rule blocked ping traffic, while restoring the rule restored connectivity.

This project provided practical experience with AWS networking, VPC Peering, route tables, security groups, EC2 instances, and network troubleshooting.

## 12. Author

AWS Cloud Computing Internship Project  
Team EWB Courses
