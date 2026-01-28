\# Architecture



\## Overview

This project demonstrates a secure and scalable static website hosting architecture on AWS using Amazon S3 and Amazon CloudFront.



The website content is stored in a private Amazon S3 bucket. All public access is served through Amazon CloudFront using HTTPS. Direct access to the S3 bucket is blocked.



\## Architecture Flow



User (Browser)  

→ HTTPS request  

→ Amazon CloudFront (CDN)  

→ Origin Access Control (OAC)  

→ Private Amazon S3 Bucket (Static Website Files)



Direct public access to the S3 bucket is blocked.



\## Components Used



\### Amazon S3

\- Stores static website files (HTML, CSS, JS, images).

\- Public access is fully blocked.

\- Bucket policy allows access only from CloudFront using Origin Access Control (OAC).



\### Amazon CloudFront

\- Acts as a Content Delivery Network (CDN).

\- Serves content over HTTPS.

\- Uses Origin Access Control (OAC) to securely access S3.

\- Caches content globally for low latency.

\- Redirects HTTP traffic to HTTPS.



\### Lifecycle Management

\- Lifecycle rules are configured to delete old object versions automatically.

\- Prevents unnecessary storage costs.



\## Benefits of This Architecture

\- High security (private S3, HTTPS only)

\- High performance (CloudFront caching)

\- Low cost (AWS Free Tier friendly)

\- Scalable (can handle large traffic easily)

\- Production-style setup



\## Architecture Diagram

Refer to the architecture diagram in the `diagram/` folder or the PDF documentation in `docs/`.



