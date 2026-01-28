# AWS Secure Static Website Hosting

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Amazon S3](https://img.shields.io/badge/S3-%23569A31.svg?style=for-the-badge&logo=amazons3&logoColor=white)
![CloudFront](https://img.shields.io/badge/CloudFront-%238C4FFF.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

## 🌐 Live Demo
**Website URL:** [https://d2ved99pwlg9sq.cloudfront.net](https://d2ved99pwlg9sq.cloudfront.net)

---

## 📌 Project Overview
This project demonstrates how to securely host a static website on AWS using industry best practices. The website is stored in an **Amazon S3** bucket and delivered globally using **Amazon CloudFront** with HTTPS, private bucket access, caching, and lifecycle management.

**Goal:** To showcase secure cloud infrastructure design, CDN content delivery, cost optimization, and production-style hosting.

📄 **[View Full Technical Report (PDF)](docs/technical-report.pdf)**

---

## 🏗️ Architecture
**Flow:** `User` → `CloudFront (CDN + HTTPS)` → `Private S3 Bucket`

CloudFront acts as the secure entry point and fetches content from S3 using **Origin Access Control (OAC)**. Direct public access to the S3 bucket is completely blocked.

![Architecture Diagram](diagram/architecture.png)
*(Note: Architecture diagram placeholder)*

---

## ☁️ AWS Services Used

| Service | Purpose |
| :--- | :--- |
| **Amazon S3** | Static website storage (HTML, CSS). |
| **Amazon CloudFront** | Content Delivery Network (CDN) & HTTPS termination. |
| **AWS IAM / Policies** | Secure access control via Bucket Policies. |
| **S3 Lifecycle Rules** | Cost optimization by managing object versions. |
| **CloudFront OAC** | Restricting S3 access to CloudFront identities only. |

---

## 🔐 Security Features
* ✅ **Zero Public Access:** S3 public access is completely blocked.
* ✅ **Origin Access Control (OAC):** Only CloudFront is allowed to read from S3.
* ✅ **Encryption:** HTTPS enforced; HTTP automatically redirected to HTTPS.
* ✅ **Least Privilege:** Only `GET` and `HEAD` methods allowed (no write access).
* ✅ **Security:** No credentials stored in the repository.

---

## 💰 Cost Control
> This project is designed to utilize **AWS Free Tier** services.

* **Serverless:** No EC2, RDS, or Lambda costs.
* **Storage Optimization:** Lifecycle rules delete old object versions automatically.
* **Request Reduction:** CloudFront caching reduces the number of requests to S3.
* **Logging:** Intentionally disabled to avoid extra storage charges.

---

## 📂 Project Structure
```bash
aws-secure-static-site/
├── 📄 website/         # Static website files (HTML, CSS)
├── 📷 screenshots/     # Architecture & AWS console screenshots
├── 📐 diagram/         # Architecture and flow diagrams
├── 📘 docs/            # Technical documentation and PDF
└── 📜 README.md        # Project documentation
Deployment Steps (High Level)
The following steps were taken to build this infrastructure:

[x] Create an S3 bucket

[x] Upload static website files

[x] Enable static website hosting

[x] Create CloudFront distribution

[x] Configure Origin Access Control (OAC)

[x] Block public S3 access

[x] Apply bucket policy for CloudFront

[x] Enable HTTPS redirect & configure caching

[x] Set Lifecycle rules

[x] Invalidate cache for content refresh

🖼️ Screenshots
Configuration evidence is available in the screenshots/ folder.

<details> <summary>Click to view Screenshot list</summary>

S3 static hosting configuration

CloudFront distribution details

Bucket policy settings

Cache invalidation

Lifecycle rule configuration

</details>

📚 What I Learned
How CDNs (CloudFront) improve performance and security.

The critical difference between public and private S3 buckets.

Securing S3 origins using Origin Access Control (OAC).

Cost optimization techniques using Lifecycle rules.

Production-style hosting workflows.

🔮 Future Improvements
[ ] Add Custom Domain (Route 53)

[ ] Add WAF Protection

[ ] Implement CI/CD using GitHub Actions

[ ] Enable Access Logging

[ ] Automate infrastructure with Terraform

⚠️ Disclaimer
The website content is used only for learning and infrastructure demonstration purposes. This project focuses on cloud deployment and security, not website development.

👨‍💻 Author
Cholan Kinnera Cloud & AWS Learner