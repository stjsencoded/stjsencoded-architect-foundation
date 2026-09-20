<p align="center">
  <img src="ST. JS ENCODED YouTube Logo.png" alt="ST. JS ENCODED Logo" width="200">
</p>

📘 ST. JS ENCODED — Multi‑Tier Cloud Architecture (AWS)
A Production‑Inspired, Secure, Highly Available Application Deployment
1. Problem Statement
Modern applications — especially those supporting a multimedia brand like ST. JS ENCODED™ — require more than simple hosting. They must be:
Highly available (survive failures)
Scalable (handle growth)
Secure (protect data and internal services)
Observable (monitored and logged)
Layered (separation of web, app, and data tiers)
Most beginners deploy a single EC2 instance or a simple static site. This creates critical issues:
No fault tolerance
No separation of concerns
Public exposure of sensitive components
No scaling
No monitoring
No production readiness
The problem: How do we design a real, production‑grade, multi‑tier architecture that demonstrates Cloud Architect thinking — not student-level deployment?
2. Solution Overview
This project implements a three‑tier AWS architecture built for:
High availability
Scalability
Security
Operational visibility
Architectural clarity
The Solution: A Multi‑Tier Cloud Architecture
Tier 1 — Presentation Layer
CloudFront (optional CDN)
Application Load Balancer (public entry point)
Tier 2 — Application Layer
EC2 Auto Scaling Group
EC2 instances in private subnets
IAM roles for secure access
Security Groups enforcing least privilege
Tier 3 — Data Layer
Amazon RDS (MySQL or Aurora)
Private subnets
Multi‑AZ for resilience
No public access
Shared Services
S3 (logs + static assets)
CloudWatch (metrics + alarms)
KMS (optional encryption)
VPC endpoints (optional)
This architecture mirrors real production environments used by Cloud Engineers and Solutions Architects.
3. Architecture Diagram
(Diagram will be added after VPC creation)
The diagram will include:
VPC
Public subnets
Private app subnets
Private DB subnets
IGW
NAT Gateway
ALB
Auto Scaling Group
EC2 instances
RDS
S3
CloudWatch
4. Architecture Components
VPC & Networking
VPC: 10.0.0.0/16
2 public subnets
2 private app subnets
2 private DB subnets
Internet Gateway
NAT Gateway
Route tables for public, private app, and private DB layers
Security
IAM role for EC2 (S3 + CloudWatch access)
Security Groups:
ALB SG → inbound from internet
EC2 SG → inbound only from ALB SG
RDS SG → inbound only from EC2 SG
Application Layer
Launch Template
Auto Scaling Group
EC2 instances in private subnets
ALB in public subnets
Target group + health checks
Data Layer
RDS MySQL (Multi‑AZ)
DB subnet group
Private access only
Encrypted storage (optional)
Observability
CloudWatch metrics
CloudWatch alarms
ALB access logs → S3
Optional dashboard
5. Traffic Flow
Code
Internet → CloudFront (optional) → ALB → EC2 (private subnets) → RDS (private subnets)

Outbound traffic from EC2 → NAT Gateway → Internet No inbound traffic reaches EC2 or RDS directly.
6. High Availability & Scalability
Multi‑AZ subnets
ALB distributes traffic
Auto Scaling Group adjusts capacity
RDS Multi‑AZ failover
This architecture survives:
EC2 instance failure
AZ failure
Traffic spikes
7. Security Considerations
No public EC2
No public RDS
IAM roles instead of SSH keys
Security Groups enforce least privilege
Optional KMS encryption
Optional Secrets Manager for DB credentials
8. Monitoring & Logging
CloudWatch alarms for:
EC2 CPU
ALB 5xx errors
RDS connections
ALB access logs → S3
Optional CloudWatch dashboard
9. Cost Considerations
NAT Gateway (hourly + data)
RDS Multi‑AZ (higher cost but required for HA)
EC2 instances (size depends on app)
ALB (hourly + LCU)
S3 (minimal cost)
CloudWatch (alarms + logs)
You will document cost‑saving alternatives later.
10. Future Improvements
Add AWS WAF
Add VPC endpoints (S3, DynamoDB)
Add EC2 Instance Connect Endpoint
Migrate app tier to ECS or Lambda
Add CI/CD pipeline
Add Secrets Manager
Add CloudFront + ACM certificate
11. Repository Structure
Code
/architecture-diagram
/docs
/src
README.md

12. Purpose of This Project
This project proves you can:
Design a real AWS architecture
Explain your decisions
Build secure network boundaries
Deploy scalable compute
Manage a relational database
Implement monitoring
Communicate like a Cloud Architect
