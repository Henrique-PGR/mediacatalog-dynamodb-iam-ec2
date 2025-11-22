DynamoDB Read-Only Access from EC2 (Console, CLI, and CloudFormation)
Author: Will A. Soto — Cloud DevOps Engineer ☁️
Overview

This project demonstrates three different deployment methods (AWS Console, AWS CLI, and CloudFormation) to implement a secure, read-only DynamoDB architecture accessed from an EC2 instance using an IAM instance profile — with no stored credentials on the instance.

This mirrors real DevOps workflows:

Prototype manually

Automate via CLI

Standardize with IaC

Architecture Summary

DynamoDB table storing classic movie metadata

EC2 instance running Amazon Linux 2023

IAM role with read-only DynamoDB permissions

No access keys stored on the instance

Public subnet + security group allowing SSH from trusted IP

Deployed three different ways (Console, CLI, CloudFormation)

Repository Contents
mediacatalog-dynamodb-iam-ec2/
│
├── ec2-trust-policy.json
├── mediacatalog-cli-read-policy.json
├── mediacatalog-cf.yaml
├── movies-cf-batch.json
│
└── validation-screenshots/
    ├── 01-dynamodb-console-scan-mediacatalog.png
    ├── 02-iam-policy-readonly-dynamodb.png
    ├── 03-ec2-console-mediacatalog-reader.png
    ├── 04-ec2-cli-dynamodb-scan.png
    ├── 05-ec2-cli-putitem-access-denied.png
    ├── 06-local-cli-dynamodb-scan-mediacatalogcli.png
    ├── 07-cli-ec2-runinstances-mediacatalogcli.png
    ├── 08-ec2-mediacatalogcli-scan-and-putitem-error.png
    ├── 09-cloudformation-stack-create-complete.png
    └── 10-ec2-cloudformation-mediacatalogcf-ec2.png

Deployment Methods
1. AWS Console (Hands-On Validation)

Created DynamoDB table MediaCatalog

Attached read-only IAM policy

Launched EC2 instance with MediaCatalogReadRole

Verified:

Scan allowed

PutItem denied

No credentials stored on instance

2. AWS CLI (Fully Scripted Deployment)

Used CLI commands to automate:

aws dynamodb create-table
aws dynamodb batch-write-item
aws iam create-role
aws iam put-role-policy
aws ec2 run-instances


Ensures repeatability and automation readiness.

3. CloudFormation (Infrastructure-as-Code)

CloudFormation template (mediacatalog-cf.yaml) provisions:

DynamoDB table

IAM role + instance profile

EC2 instance

Security group

All deployed in a single IaC workflow.

Validation Results

Across all three deployment methods:

✅ DynamoDB scan works

❌ PutItem fails with AccessDenied (intended)

✅ EC2 uses IAM instance profile, not access keys

✅ Architecture is identical across Console, CLI, and CloudFormation

📸 All proof stored in validation-screenshots/

Concluding Insights

Delivering the same architecture through Console, CLI, and CloudFormation demonstrates versatility across operational, automated, and IaC-based cloud workflows.
This repository serves as a reusable blueprint for secure, read-only DynamoDB access patterns in AWS.
