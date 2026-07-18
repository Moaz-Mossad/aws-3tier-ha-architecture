# SecureWeb — 3-Tier AWS Architecture

A highly available, secure e-commerce architecture built on AWS.

## Architecture Diagram
<p align="center">
  <img src="architecture-diagram.png" alt="SecureWeb Architecture Diagram" width="800">
  <p align="center">
  <img width="600" alt="architecture-diagram" src="https://github.com/user-attachments/assets/21c76da4-dc41-4943-9abd-2a33d4c8b6f8" />
</p>

  
</p>


--> Architecture Overview
 Deploy a production-grade web application (Route 53) on AWS using EC2 instances inside a properly architected VPC with public and private subnets across two Availability Zones. Achieve high availability and scalability with ALB, ASG, and a CloudFront distribution for caching static assets. A Multi-AZ RDS instance serves as the database backend, with all compute in private subnets.

--> Services Used
- Route 53 – DNS resolution, alias record to CloudFront
- CloudFront– CDN, caches static assets, reduces latency
- WAf– Filters malicious traffic (OWASP Top 10) before reaching ALB
- ALB – Layer 7 load balancing across EC2 instances in 2 AZs
- Auto Scaling Group– Automatically scales EC2 based on CPU target tracking
- EC2 – Application layer, private subnet, no public IP
- RDS Multi-AZ – MySQL/PostgreSQL with automatic failover
- NAT Gateway – Outbound-only internet access for private resources
- Systems Manager (SSM)– Secure instance access without SSH/key pairs

--> Design Decisions
- RDS is isolated in its own private subnet, separate from EC2, for tighter security-group and NACL control
- SSM Session Manager used instead of SSH to eliminate open inbound ports entirely
- Multi-AZ RDS ensures automatic failover with zero manual intervention
- NAT Gateway allows private EC2 instances to reach the internet for updates without being publicly reachable
