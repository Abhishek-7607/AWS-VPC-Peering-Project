# AWS-VPC-Peering-Project
AWS VPC Peering project demonstrating private communication between two VPCs.

# AWS VPC Peering Project

## Project Overview

This project demonstrates private communication between two Amazon Virtual Private Clouds (VPCs) using AWS VPC Peering.

The project was completed as part of AWS Cloud Computing practical learning.

## Objectives

- Create two VPCs with non-overlapping CIDR blocks.
- Configure public and private subnets.
- Establish a VPC Peering connection.
- Configure route tables for communication between VPCs.
- Configure security groups to control network traffic.
- Launch and connect to EC2 instances.
- Test connectivity using private IP addresses.
- Verify the effect of security group rules on ICMP traffic.

## AWS Services Used

- Amazon VPC
- VPC Peering
- Amazon EC2
- Route Tables
- Internet Gateway
- Security Groups
- Amazon Linux 2023

## Network Configuration

### VPC A

| Resource | Configuration |
|---|---|
| VPC Name | ewb-vpc-a |
| CIDR Block | 10.10.0.0/16 |
| Public Subnet | ewb-a-public |
| Public Subnet CIDR | 10.10.1.0/24 |
| Private Subnet | ewb-a-private |
| Private Subnet CIDR | 10.10.2.0/24 |

### VPC B

| Resource | Configuration |
|---|---|
| VPC Name | ewb-vpc-b |
| CIDR Block | 10.20.0.0/16 |
| Private Subnet | ewb-b-private |
| Private Subnet CIDR | 10.20.1.0/24 |

## EC2 Instances

| Instance | Private IP | Purpose |
|---|---|---|
| ewb-bastion | 10.10.1.10 | Secure access to private instances |
| ewb-app-a | 10.10.2.10 | Application instance in VPC A |
| ewb-app-b | 10.20.1.10 | Application instance in VPC B |

The application instances communicate using their private IP addresses.

## Implementation Steps

1. Created VPC A and VPC B.
2. Created the required subnets.
3. Attached an Internet Gateway to VPC A.
4. Created and accepted the VPC Peering connection.
5. Added the required routes to the route tables.
6. Configured security groups for SSH and ICMP traffic.
7. Launched the EC2 instances.
8. Connected to the private instances through the Bastion host.
9. Tested connectivity between App-A and App-B.

## Routing Configuration

### VPC A Private Route Table

- `10.10.0.0/16` — Local route
- `10.20.0.0/16` — VPC Peering connection

### VPC B Private Route Table

- `10.20.0.0/16` — Local route
- `10.10.0.0/16` — VPC Peering connection

The public route table in VPC A also includes a default route to the Internet Gateway and a route to VPC B through the peering connection.

## Connectivity Testing

### Test 1: App-A to App-B

Command:

`ping -c 4 10.20.1.10`

Result: Successful — 4 packets transmitted, 4 received, 0% packet loss.

### Test 2: App-B to App-A

Command:

`ping -c 4 10.10.2.10`

Result: Successful — 4 packets transmitted, 4 received, 0% packet loss.

### Test 3: ICMP Rule Removed

The inbound ICMP rule on the App-B security group was temporarily removed.

Result: Ping failed with 100% packet loss.

### Test 4: ICMP Rule Restored

The inbound ICMP rule was restored and connectivity was tested again.

Result: Ping succeeded with 0% packet loss.

## Screenshots and Evidence

Project screenshots are available in the [`screenshots`](./screenshots/) folder.

The evidence includes VPC configuration, subnets, route tables, the peering connection, security groups, EC2 instances, SSH access, and connectivity testing.

## Conclusion

The project successfully demonstrated private communication between two AWS VPCs using VPC Peering.

Connectivity was verified in both directions using private IP addresses. The ICMP security test also demonstrated how security group rules can block and restore network traffic.

This project provided practical experience with AWS networking, VPC Peering, routing, security groups, EC2, and troubleshooting.

## Author

AWS Cloud Computing Internship Project  
Team EWB Courses
