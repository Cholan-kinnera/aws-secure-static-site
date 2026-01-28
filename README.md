"AWS Secure Static Website Hosting":

 Project Overview:

This project demonstrates how to securely host a static website on AWS using industry best practices.
The website is stored in an Amazon S3 bucket and delivered globally using Amazon CloudFront with HTTPS, private bucket access, caching, and lifecycle management.

The goal of this project is to learn and showcase:
• Secure cloud infrastructure design
• Content delivery using CDN
• Cost-aware cloud configuration
• Production-style static website hosting

Architecture:

User → CloudFront (CDN + HTTPS) → Private S3 Bucket (Static Website)

CloudFront acts as a secure entry point and fetches content from S3 using Origin Access Control (OAC).
Direct public access to the S3 bucket is blocked.

AWS Services Used:

• Amazon S3 – Static website storage
• Amazon CloudFront – Content Delivery Network (CDN)
• AWS IAM / Bucket Policy – Secure access control
• S3 Lifecycle Rules – Cost optimization
• CloudFront Cache Invalidation – Content refresh
• HTTPS (TLS) – Secure data delivery

Security Features Implemented:

• S3 public access completely blocked
• Only CloudFront is allowed to read from S3 (Origin Access Control)
• HTTPS enforced using CloudFront
• HTTP automatically redirected to HTTPS
• Only GET and HEAD methods allowed
• No write access exposed
• No credentials stored in repository

Cost Control:

• Uses AWS Free Tier services
• No EC2, no RDS, no Lambda
• Lifecycle rule deletes old object versions
• Logging disabled to avoid extra charges
• CloudFront caching reduces S3 requests

Project Structure:

aws-secure-static-site/
├── website/        # Static website files (HTML, CSS)
├── screenshots/    # Architecture & AWS console screenshots
├── docs/           # Optional documentation
└── README.md       # Project documentation

Screenshots:

Screenshots are available in the screenshots/ folder:

• S3 static hosting configuration
• CloudFront distribution
• Bucket policy
• Cache invalidation

Lifecycle rule

Deployment Steps (High Level):

• Create an S3 bucket
• Upload static website files
• Enable static website hosting
• Create CloudFront distribution
• Configure S3 Origin Access Control
• Block public S3 access
• Apply bucket policy for CloudFront
• Enable HTTPS redirect
• Configure cache behavior
• Set lifecycle rule
• Invalidate cache

What I Learned:

• How CDN improves performance and security
• How to secure S3 using CloudFront OAC
• Difference between public and private buckets
• How caching works
• Cost optimization techniques
• Production-style hosting workflow


Documentation:

Full technical documentation is available here:  
[Project Report (PDF)](docs/AWS_Secure_Static_Website_Hosting.pdf)

Architecture:
[Architecture](diagram/flow.png)

Disclaimer:

• The website content is used only for learning and infrastructure demonstration purposes.
• This project focuses on cloud deployment and security, not website development.

Author:

Cholan Kinnera
Cloud & AWS Learner

Future Improvements:

• Add custom domain
• Add WAF protection
• Add CI/CD using GitHub Actions
• Enable access logging
• Terraform automation