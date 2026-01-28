# 🏗️ System Architecture

## Overview
This project demonstrates a secure and scalable static website hosting architecture on AWS. The solution leverages **Amazon CloudFront** for global content delivery and **Amazon S3** for secure storage.

The core design principle is **"Zero-Trust Origin"**: the S3 bucket is completely private, and all traffic is forced through the CloudFront CDN using secure, authenticated requests.

## 🔄 Architecture Flow

**User** (Browser)
   ↓
   *(HTTPS Request)*
   ↓
**Amazon CloudFront** (CDN & Edge Caching)
   ↓
   *(Origin Access Control - SigV4)*
   ↓
**Private Amazon S3 Bucket** (Static Assets)

> **Note:** Direct public access to the S3 bucket is strictly blocked. Users cannot bypass the CDN.

## 🧩 Components

### 1. Amazon S3 (Storage Layer)
* **Purpose:** Stores the static website files (HTML, CSS, JS).
* **Security:** "Block All Public Access" is enabled. The bucket is not accessible via the public internet.
* **Access Control:** A Bucket Policy is applied that only allows read access (`s3:GetObject`) from the specific CloudFront distribution.

### 2. Amazon CloudFront (Delivery Layer)
* **Purpose:** Acts as the Content Delivery Network (CDN) to serve the website globally with low latency.
* **Security:** Enforces HTTPS for all connections and redirects HTTP traffic automatically.
* **Origin Access Control (OAC):** Authenticates requests to the S3 origin, ensuring only valid CloudFront requests are processed.

### 3. Lifecycle Management
* **Cost Optimization:** Automated rules are configured to delete non-current object versions after a set period.
* **Storage Health:** Prevents storage costs from growing unnecessarily due to file updates.

## 🛡️ Key Features

### Security
* **Private Origin:** The S3 bucket URL returns `403 Forbidden` to anyone trying to access it directly.
* **Encryption:** All data in transit is encrypted via TLS 1.2/1.3.
* **Least Privilege:** IAM policies are restricted to only allow necessary read operations.

### Performance & Scalability
* **Edge Caching:** Content is cached at AWS Edge Locations closer to the user, significantly reducing load times.
* **Serverless:** The architecture automatically scales to handle traffic spikes without manual intervention.