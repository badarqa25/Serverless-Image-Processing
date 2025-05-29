# Serverless Image Processing System using AWS Lambda & Amazon S3

This project implements an automated serverless image processing system using **AWS Lambda** and **Amazon S3**. It processes uploaded images by resizing, watermarking, or converting formats whenever a new file is added to the S3 source bucket.

## Features

- Automatically triggered when a new image is uploaded to S3
- Image processing handled by AWS Lambda (written in Python)
- Fully serverless (no need to manage servers)
- Uses IAM for secure permission control
- Real-time logs in AWS CloudWatch

---

## 📁 Architecture

1. **Source S3 Bucket**: `source-bucket-by-badarqa`  
   User uploads go here.

2. **AWS Lambda Function**: `ImageProcessor`  
   Processes the image (resize, watermark, convert).

3. **Destination S3 Bucket** *(optional)*: e.g., `processed-bucket-by-badarqa`  
   Stores the processed output (if used).

---

##  How It Works

1. A user uploads an image to the source bucket.
2. The upload event triggers the Lambda function.
3. The Lambda function processes the image and (optionally) saves it to a destination bucket.

---

## 🔧 Setup Guide (via AWS CloudShell)

### 1. Create IAM Role and Attach Policies

```bash
aws iam create-role --role-name lambda-s3-execute-role \
  --assume-role-policy-document file://trust-policy.json

aws iam attach-role-policy --role-name lambda-s3-execute-role \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess

aws iam attach-role-policy --role-name lambda-s3-execute-role \
  --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole

