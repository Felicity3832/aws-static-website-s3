# AWS Static Website with Amazon S3 and CloudFront

## Project Overview

This project demonstrates how to deploy and manage a static website using Amazon S3 and Amazon CloudFront.

The project was built as part of my hands-on AWS and DevOps learning journey. It covers Amazon S3 static website hosting, IAM permissions, least-privilege access, CloudFront content delivery, regional infrastructure, and basic AWS troubleshooting.

## Architecture

The website follows this architecture:

**User → Amazon CloudFront → Amazon S3 → index.html**

CloudFront provides a global content delivery layer in front of the S3 static website.

The S3 bucket is hosted in the `eu-north-1` (Europe/Stockholm) AWS Region, while CloudFront provides global access to the website.

## AWS Services Used

* Amazon S3
* Amazon CloudFront
* AWS IAM

## Project Components

### 1. HTML Website

Created a simple `index.html` file containing the website content.

### 2. S3 Bucket

Created an Amazon S3 bucket named:

`student-lab-felicity`

The bucket is hosted in the `eu-north-1` (Europe/Stockholm) AWS Region.

### 3. IAM Least-Privilege Policy

Created a custom IAM policy that provides only the permissions required to manage the website:

* `s3:ListBucket`
* `s3:GetObject`
* `s3:PutObject`

The policy was scoped specifically to the project bucket rather than granting access to all S3 buckets.

The policy is included in this repository as:

`policy.json`

### 4. Static Website Hosting

Enabled S3 Static Website Hosting and configured:

* Index document: `index.html`

### 5. Bucket Policy

Configured an S3 bucket policy to allow public read access to website objects so visitors can access the website.

### 6. CloudFront Distribution

Created an Amazon CloudFront distribution to deliver the website through a global content delivery network.

Configured:

* S3 static website endpoint as the origin
* Origin protocol: HTTP only
* Viewer protocol policy: Redirect HTTP to HTTPS

The CloudFront distribution provides a global access layer while the S3 bucket remains hosted in the Stockholm AWS Region.

## Deployment Steps

1. Created an IAM user for the AWS lab.
2. Created a custom least-privilege S3 IAM policy.
3. Created the `student-lab-felicity` S3 bucket.
4. Created the `index.html` website file locally using VS Code.
5. Uploaded the website file to the S3 bucket.
6. Enabled S3 Static Website Hosting.
7. Configured the bucket policy for public read access.
8. Tested the website using the S3 static website endpoint.
9. Created a CloudFront distribution using the S3 website endpoint as the origin.
10. Configured CloudFront to redirect HTTP viewer requests to HTTPS.
11. Tested the website using the CloudFront distribution domain.
12. Compared access to the regional S3 bucket and globally accessible CloudFront distribution.

## Troubleshooting

### 403 AccessDenied

During the initial deployment, the website returned a `403 AccessDenied` error.

The issue was investigated by checking the S3 bucket permissions and IAM configuration.

The bucket's public access settings were verified, and a bucket policy was configured to allow public `s3:GetObject` access to the website objects.

After updating the configuration, the website became accessible through the S3 static website endpoint.

### CloudFront 504 Gateway Timeout

During the CloudFront setup, the distribution initially returned a `504 Gateway Timeout` error.

The CloudFront origin configuration was checked to ensure that the S3 static website endpoint was being used and that the origin protocol was set to HTTP only.

After correcting the configuration, CloudFront successfully served the website.

## Regional Infrastructure and Global Access

The S3 bucket is located in the **Europe (Stockholm) — `eu-north-1`** AWS Region.

When the AWS Console was changed to **Europe (London) — `eu-west-2`**, the S3 bucket was not available in the regional bucket view because S3 resources are associated with specific AWS Regions.

However, the CloudFront distribution remained accessible and continued serving the website.

This demonstrated the difference between regional AWS services such as S3 and global services such as CloudFront.

## What I Learned

Through this project, I gained practical experience with:

* Creating and managing S3 buckets
* Hosting static websites on Amazon S3
* Understanding IAM users and policies
* Applying the principle of least privilege
* Writing IAM policies using JSON
* Understanding the difference between IAM permissions and S3 bucket policies
* Troubleshooting S3 `403 AccessDenied` errors
* Configuring Amazon CloudFront
* Using an S3 static website endpoint as a CloudFront origin
* Configuring HTTP to HTTPS redirection
* Understanding regional versus global AWS infrastructure
* Troubleshooting CloudFront `504 Gateway Timeout` errors
* Deploying and delivering a website using multiple AWS services

## Website Screenshots

### S3 Static Website

### CloudFront Distribution

## Live Website

[S3 Static Website](http://student-lab-felicity.s3-website.eu-north-1.amazonaws.com)

[CloudFront Distribution](https://dvgml42pr8s2j.cloudfront.net/)
