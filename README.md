# Project 23 – IAM Role-Based Access

## Objective
Configure an EC2 instance with an IAM role to access an existing
Amazon S3 bucket without storing AWS access keys on the instance.

## AWS Configuration
- AWS Account: 590507089733
- Region: ap-south-1 (Mumbai)
- EC2 Instance: mb-project23-iam-test
- Instance ID: i-072d4a85095579826
- IAM Role: mb-project23-ec2-s3-role
- Instance Profile: mb-project23-ec2-s3-profile
- IAM Policy: mb-project23-s3-access-policy
- S3 Bucket: mbproject22-log-archive-2026-590507089733-ap-south-1-an

## IAM Permissions
The custom IAM policy grants:
- s3:ListBucket on the specified bucket
- s3:GetObject on objects inside the bucket

## Trust Relationship
The IAM role trusts the EC2 service (ec2.amazonaws.com).

## CLI Validation
Tests were successfully executed inside the EC2 instance
using AWS Systems Manager Session Manager.

### 1. Verify IAM Role
Command:
aws sts get-caller-identity

Expected identity:
assumed-role/mb-project23-ec2-s3-role

### 2. Test S3 List Access
Command:
aws s3 ls s3://mbproject22-log-archive-2026-590507089733-ap-south-1-an/

Result: Successful bucket listing.

### 3. Test S3 Object Download
Command:
aws s3 cp s3://mbproject22-log-archive-2026-590507089733-ap-south-1-an/logs/application.log /tmp/application.log

Result: Successful download.

### 4. Verify Downloaded File
Command:
ls -l /tmp/application.log

Result: File downloaded successfully (183 bytes).

## Screenshots
See the screenshots/ directory for CLI proof.

## Security Notes
- No IAM access keys were stored on the EC2 instance.
- The EC2 instance uses an attached IAM role.
- The IAM policy follows least-privilege access for the specified S3 bucket.
- Private SSH keys and credentials are excluded from this repository.
