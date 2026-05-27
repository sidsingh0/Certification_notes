# AWS Notes by Service

## CloudFront
- Speeds up live streaming and on-demand video.
- Can use multiple origins based on path (`/img/` → S3, `/api/` → ALB).
- Only supports HTTP/HTTPS (no TCP/UDP).
- **Tip:** Don’t put Global Accelerator in front—caching breaks.

## Global Accelerator
- Optimized for TCP/UDP traffic to EC2 or load balancers.
- Not meant to front CloudFront.

## Route 53
- Handles multi-region load balancing.

## ALB (Application Load Balancer)
- Single-region load balancing.
- Integrates with AWS WAF (Layer 7).

## EC2 & Compute
- **Spot Instances:** For stateless or interruptible workloads.
- **Lambda:** Not for image processing or large files.
- **Amplify:** Build web/mobile apps (not for migrations).

## S3
- **Inventory:** Audit/report bucket contents (needs Batch Operations to act).
- **Event Notifications:** Can trigger Lambda, SQS, SNS, EventBridge.
- **File Gateway:** Better than mount points due to caching.
- Block storage uses iSCSI, therefore use volume gateway

## RDS / Aurora
- Snapshots are service-level, **not** auto-stored in S3.
- Integrated with KMS for encryption.
- Aurora auto-scaling slower than DynamoDB.

## Database Migration
- **DMS:** Migrate same engine; ongoing replication = zero downtime.
- **Schema Conversion Tool:** Migrate different engines.

## Migration (Lift & Shift)
- Use **AWS Application Migration Service**:
  - Install replication agent on VM.
  - Complete initial replication and test instances.
  - Stop on-prem VMs and launch cutover instance.
- **Direct Connect:** Connect on-premises to AWS.

## Networking & VPC
- **VPC Peering:** Connects **whole VPCs**, not single machines.
- **Virtual Private Gateway:** Connects VPC to on-prem via VPN or Direct Connect.
- **VPC Gateway Endpoints:** Access AWS services from VPC (S3, DynamoDB).
- **Interface Endpoints:** Paid service.
- **DNS:** Usually UDP.
- **Egress-Only IGW:** IPv6 only, cheaper.
- **NAT Gateway:** IPv4 traffic.
- HTTPS protects data from internet, not from our internal application stack logging after tls termination
	- We can use field level encryption in cloudfront to protect data from being logged too after tls termination

## Security
- **AWS Shield:** Layer 3/4 (NLB protection).
- **AWS WAF:** Layer 7 (ALB, API Gateway).
- Managed services like API Gateway, ALB, S3 **don’t have security groups**.
- We cannot reference security group ids, if the security groups are in different regions.
- **IRSA:** Manages EKS pod permissions.

## Monitoring
- **CloudWatch Logs:** Can feed directly into OpenSearch.

## Disaster Recovery
- **Pilot Light:** Minimal resources, slower recovery (minutes to hours).
- **Warm Standby:** Reduced-capacity live system, faster recovery (minutes).

## API Gateway
- **Private integration:** Connect internal VPC resources.

# Elastic Beanstalk
- Has support for URL swapping for blue green testing to test different versions/features of app