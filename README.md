AWS Secure Static Website Hosting

Overview



This project demonstrates a secure, scalable, and cost-efficient static website hosting architecture on AWS, designed using industry best practices. The website is hosted in a private Amazon S3 bucket and delivered globally via Amazon CloudFront over HTTPS, ensuring security, performance, and controlled access.



The primary objective of this project is to learn and showcase real-world cloud infrastructure design, focusing on security hardening, CDN-based content delivery, and cost optimization.



Architecture Overview



Request Flow:



User (Browser)

   ↓ HTTPS

Amazon CloudFront (CDN)

   ↓ Origin Access Control (OAC)

Private Amazon S3 Bucket (Static Website Files)





CloudFront acts as the secure entry point for all requests.

Direct public access to the S3 bucket is completely blocked, and objects are served only through CloudFront using Origin Access Control.



Architecture Diagram



A detailed architecture diagram is included in the documentation:



docs/AWS\_Secure\_Static\_Website\_Hosting.pdf



diagram/flow.png



AWS Services Used



Amazon S3 – Static website storage (private bucket)



Amazon CloudFront – Global CDN with HTTPS enforcement



AWS IAM \& Bucket Policy – Secure origin access using OAC



S3 Lifecycle Rules – Automatic cleanup of non-current object versions



CloudFront Cache Invalidation – Content refresh control



Security Implementation



This project follows a security-first approach:



S3 public access fully blocked



CloudFront is the only allowed reader of S3 objects (OAC)



HTTPS enforced using CloudFront



HTTP automatically redirected to HTTPS



Only GET and HEAD methods allowed



No credentials, secrets, or keys stored in the repository



Cost Optimization



Uses AWS Free Tier–eligible services



No EC2, RDS, Lambda, or paid backend services



CloudFront caching minimizes S3 request costs



Lifecycle rules delete old object versions automatically



Logging intentionally disabled to avoid unnecessary charges



Repository Structure

aws-secure-static-site/

├── website/        # Static website files (HTML, robots.txt, sitemap.xml)

├── screenshots/    # AWS console and configuration screenshots

├── diagram/        # Architecture and flow diagrams

├── docs/           # Detailed documentation and PDF

├── README.md       # Project overview and documentation



Screenshots



Configuration screenshots are available in the screenshots/ directory, including:



S3 static website configuration



CloudFront distribution setup



Bucket policy with Origin Access Control



Cache invalidation



Lifecycle rule configuration



Deployment Summary (High Level)



Create a private S3 bucket



Upload static website files



Enable static website hosting



Create a CloudFront distribution



Configure Origin Access Control (OAC)



Block all public access to S3



Enforce HTTPS and caching



Apply lifecycle rules



Perform cache invalidation



Learning Outcomes



Designing secure cloud architectures



Implementing private S3 access with CloudFront



Applying CDN caching and HTTPS enforcement



Cost-aware infrastructure decisions



Structuring and documenting real-world cloud projects



Disclaimer



The website content used in this project is for learning and demonstration purposes only.

The focus of this repository is cloud infrastructure design and security, not website ownership.

