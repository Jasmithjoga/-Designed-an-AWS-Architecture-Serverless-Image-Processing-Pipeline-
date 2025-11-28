# -Designed-an-AWS-Architecture-Serverless-Image-Processing-Pipeline-
Serverless Image Processing Pipeline (AWS)

A fully serverless, auto-scaling image-processing architecture built using Amazon Web Services.
This project automatically resizes images when they are uploaded to an S3 bucket, stores processed images in another bucket, and optionally logs metadata in DynamoDB. All logs are captured in CloudWatch.

🚀 Project Overview
This project implements a Serverless Image Processing Pipeline as described in the assignment (INT330 CA-2) 
How it works

A user uploads an image to the Source S3 Bucket.

The upload event triggers an AWS Lambda function.

Lambda resizes/optimizes the image.

The processed image is saved in a Destination S3 Bucket.

(Optional) Metadata such as filename or format is stored in DynamoDB.

CloudWatch records all logs for monitoring.

This architecture is scalable, cost-effective, and requires no servers to manage.


🚩AWS Services Used
Core AWS Services

Amazon S3 – stores original and processed images

AWS Lambda – performs automatic image resizing

Amazon DynamoDB (optional) – stores image metadata

Amazon CloudWatch – logs all Lambda executions

AWS IAM – secure permissions for Lambda & S3

Optional Advanced Services

Amazon CloudFront – global CDN for processed images

AWS API Gateway – if exposing APIs for uploads

AWS WAF / Shield – security & protection

AWS CodePipeline – for CI/CD of Lambda updates



🚩Architecture Diagram
User → S3 (source bucket) → Event Trigger → Lambda → S3 (processed bucket)
                                                    ↓
                                              DynamoDB (metadata)
                                                    ↓
                                               CloudWatch Logs



🔧 Lambda Function

This repository contains the code for:

✔️ Listening to S3 upload events
✔️ Resizing images (max width default = 800px)
✔️ Uploading processed images
✔️ Writing optional metadata to DynamoDB



📁 Project Structure
/
├── lambda/
│   ├── image_processor.py
│   ├── requirements.txt
│
├── README.md  ← this file



🔒 IAM Permissions Needed

Lambda execution role must have:
S3 GetObject / PutObject
S3 ListBucket
DynamoDB PutItem (if used)
CloudWatch Logs permissions



📝 Steps to Deploy
1. Create the buckets
source-bucket
processed-bucket
2. Create DynamoDB table (optional)
Partition key: ImageId (String)
3. Upload Lambda code
Zip contents of /lambda/ folder and upload through AWS Console or CLI.
4. Configure S3 Trigger
Source bucket → Event type: ObjectCreated → Destination: Lambda
5. Test
Upload any .jpg / .png to the source bucket.
Processed image will appear as:
processed-<filename>.jpg

📊 Monitoring
CloudWatch Logs automatically record:
Function starts/stops
Image dimensions
Errors
DynamoDB actions
As required in assignment’s monitoring section 


🔐 Security Measures
IAM least privilege
S3 Bucket policies
Optional WAF if exposed via API Gateway (per assignment guidelines) 


📦 Future Enhancements
Add CloudFront for global delivery
Add CodePipeline for CI/CD
Add watermarking
Add image format conversion (PNG → JPG etc.)
Use ECS Fargate for heavy image processing
