# AWS Static Website with Amazon S3

## Project Overview

This project demonstrates how to deploy and manage a static website using Amazon S3.

The project was built as part of my hands-on AWS and DevOps learning journey. It covers Amazon S3 static website hosting, IAM permissions, least-privilege access, and basic AWS troubleshooting.

## Architecture

The website follows this simple flow:

User → Amazon S3 Static Website Hosting → index.html

The `index.html` file is stored in an Amazon S3 bucket and served through the S3 static website endpoint.

## AWS Services Used

- Amazon S3
- AWS IAM

## Project Components

### 1. HTML Website

Created a simple `index.html` file containing the website content.

### 2. S3 Bucket

Created an Amazon S3 bucket named:

`student-lab-felicity`

The bucket is hosted in the `eu-north-1` (Europe/Stockholm) AWS Region.

### 3. IAM Least-Privilege Policy

Created a custom IAM policy that provides only the permissions required to manage the website:

- `s3:ListBucket`
- `s3:GetObject`
- `s3:PutObject`

The policy was scoped specifically to the project bucket rather than granting access to all S3 buckets.

### 4. Static Website Hosting

Enabled S3 Static Website Hosting and configured:

- Index document: `index.html`

### 5. Bucket Policy

Configured an S3 bucket policy to allow public read access to website objects so visitors can access the website.

## Deployment Steps

1. Created an IAM user for the AWS lab.
2. Created a custom least-privilege S3 IAM policy.
3. Created the `student-lab-felicity` S3 bucket.
4. Created the `index.html` website file locally using VS Code.
5. Uploaded the website file to the S3 bucket.
6. Enabled S3 Static Website Hosting.
7. Configured the bucket policy for public read access.
8. Tested the website using the S3 static website endpoint.

## Troubleshooting

### 403 AccessDenied

During deployment, the website initially returned a `403 AccessDenied` error.

The issue was investigated by checking the S3 bucket permissions and IAM configuration.

The bucket's public access settings were verified, and a bucket policy was configured to allow public `s3:GetObject` access to the website objects.

After updating the configuration, the website became accessible through the S3 static website endpoint.

## What I Learned

Through this project, I gained practical experience with:

- Creating and managing S3 buckets
- Hosting static websites on Amazon S3
- Understanding IAM users and policies
- Applying the principle of least privilege
- Writing IAM policies using JSON
- Understanding the difference between IAM permissions and S3 bucket policies
- Troubleshooting S3 `403 AccessDenied` errors
- Deploying a basic website using AWS services

## Live Website

[View the live website](http://student-lab-felicity.s3-website.eu-north-1.amazonaws.com)