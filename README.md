# AWS Resource Tagging Lambda Function

This repository contains a Python script designed to be deployed as an AWS Lambda function. The function automates the process of applying tags to various AWS resources, enabling better organization, cost allocation, and compliance.

---

## **Overview**

This function adds tags (key-value pairs) to the following AWS resources:
1. **S3 Buckets**
2. **RDS Instances**
3. **AppSync APIs**
4. **DynamoDB Tables**

Tags help in identifying, organizing, and managing AWS resources efficiently.

---

## **Features**
- Automatically applies predefined tags to specified resources.
- Dynamically detects DynamoDB tables containing a specific keyword in their name. (because if you have 100 of tables with different name)
- Merges existing tags with new ones for S3 buckets.
- Handles tagging for resources with ARNs, such as RDS and AppSync APIs.
- Includes error handling for missing resources or API errors.

---

## **Prerequisites**
1. **AWS Lambda Environment**
   - Ensure Python language
   - Install and package the `boto3` library (if not included in the Lambda environment).
2. **IAM Permissions**
   The Lambda execution role must have the following permissions:
   - **S3**: `s3:GetBucketTagging`, `s3:PutBucketTagging`
   - **RDS**: `rds:DescribeDBInstances`, `rds:AddTagsToResource`
   - **AppSync**: `appsync:TagResource`
   - **DynamoDB**: `dynamodb:ListTables`, `dynamodb:DescribeTable`, `dynamodb:TagResource`

---

## **How It Works**
1. **Initialization**
   - The script initializes AWS clients for S3, RDS, AppSync, and DynamoDB using the `boto3` library.

2. **Resource Tagging**
   - **S3 Buckets:** Adds or updates tags for the specified bucket.
   - **RDS Instances:** Finds the RDS instance ARN and applies the tags.
   - **AppSync APIs:** Directly applies tags using the AppSync API ARN.
   - **DynamoDB Tables:** Searches for tables containing a specific string in their name and tags them.

3. **Error Handling**
   - Logs errors for missing resources or permission issues.
   - Ensures operations continue even if tagging fails for a specific resource.

---
