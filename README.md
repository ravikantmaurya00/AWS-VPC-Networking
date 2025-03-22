# AWS-VPC-Networking
This repository provides an AWS VPC architecture setup designed for a highly available and secure cloud infrastructure. It includes public and private subnets, an Internet Gateway (IGW), NAT Gateways, and a Virtual Private Gateway (VPG) for hybrid cloud connectivity. The architecture spans multiple Availability Zones (AZs) to ensure fault tolerance and scalability.
It serves as a reference for deploying scalable, secure, and cost-efficient AWS network architectures, suitable for hosting applications, databases, and hybrid cloud environments.
## Key Features:
 - Multi-AZ Deployment for high availability
 - Public & Private Subnets for better security control
 - NAT Gateway for outbound internet access from private subnets
 - VPN Connectivity to on-premises corporate networks
 - Modular & Scalable infrastructure design
## Creating VPC in AWS with 2 public and private subnet.
  **Step 1:-** **Create a VPC**
    - Go to AWS Console → Navigate to VPC Dashboard.
    - Click Create VPC → Name it (e.g., MyVPC).
    - Choose IPv4 CIDR block: 10.0.0.0/16.
    - Choose two  Availability Zones as **us-east-1a** and **us-east-1b**
    - Enable DNS hostname support.
    - Click Create VPC.


