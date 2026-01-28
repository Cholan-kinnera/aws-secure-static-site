# AWS Secure Static Website Hosting

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Amazon S3](https://img.shields.io/badge/S3-%23569A31.svg?style=for-the-badge&logo=amazons3&logoColor=white)
![CloudFront](https://img.shields.io/badge/CloudFront-%238C4FFF.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

## 📌 Overview
This project demonstrates a secure and cost-efficient static website hosting architecture on AWS. The website content is stored in a **private Amazon S3 bucket** and delivered globally via **Amazon CloudFront** with HTTPS enforcement and restricted bucket access.

The project is documentation-driven and focuses on cloud security, access control, and CDN-based delivery using AWS Free Tier services.

---

## 🏗️ Architecture
**Flow:** `User` → `CloudFront (CDN + HTTPS)` → `Private S3 Bucket`

CloudFront acts as the secure public entry point and retrieves content from S3 using **Origin Access Control (OAC)**. Direct public access to the S3 bucket is completely blocked to ensure security.

![Architecture Diagram](diagram/architecture.png)
*(Note: Ensure your architecture diagram is named architecture.png and placed in the diagram/ folder)*

---

## ☁️ AWS Services Used

| Service | Purpose |
| :--- | :--- |
| **Amazon S3** | Secure storage for static website files (HTML, CSS, JS). |
| **Amazon CloudFront** | Global Content Delivery Network (CDN) & HTTPS termination. |
| **AWS IAM / Policies** | Origin Access Control (OAC) to restrict S3 access. |
| **S3 Lifecycle Rules** | Cost optimization by managing object versions. |

---

## 🔐 Security Features
* ✅ **Zero Public Access:** S3 public access is fully blocked.
* ✅ **Origin Access Control (OAC):** Only CloudFront is authenticated to read from the bucket.
* ✅ **Encryption in Transit:** HTTPS enforced; HTTP requests are automatically redirected.
* ✅ **Method Restriction:** Only `GET` and `HEAD` methods are allowed (no write access).
* ✅ **Security Best Practices:** No credentials are stored in the repository.

---

## 💰 Cost Control
> This project is designed to run completely within the **AWS Free Tier**.

* **Serverless:** No EC2, RDS, Lambda, or paid backend services.
* **Caching:** CloudFront caching minimizes the number of requests hitting S3.
* **Lifecycle Management:** Rules configured to delete old object versions automatically.
* **Logging:** Intentionally disabled to avoid unnecessary storage charges.

---

## 📂 Repository Structure
```bash
aws-secure-static-site/
├── 📄 website/         # Static website files (HTML, robots.txt, sitemap.xml)
├── 📷 screenshots/     # AWS console and configuration screenshots
├── 📐 diagram/         # Architecture and flow diagrams
├── 📘 docs/            # Detailed documentation and PDF
└── 📜 README.md        # Project overview and documentation
Deployment Summary
The following steps were taken to deploy this infrastructure:

[x] Create a private S3 bucket

[x] Upload static website files

[x] Enable static website hosting settings

[x] Create CloudFront distribution

[x] Configure Origin Access Control (OAC)

[x] Block all public access to S3

[x] Enforce HTTPS and caching policies

[x] Apply S3 Lifecycle rules

🖼️ Screenshots
Configuration evidence is available in the screenshots/ directory:

S3 Configuration: Static website hosting settings.

CloudFront Setup: Distribution details and OAC setup.

Security: Bucket policy and Block Public Access settings.

Optimization: Cache invalidation and Lifecycle rules.

👨‍💻 Author
Cholan Kinnera Cloud & AWS Learner