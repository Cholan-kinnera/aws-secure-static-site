# 🛡️ Security Implementation

## 📌 Overview
This project prioritizes the secure delivery of static content by adhering to AWS "Well-Architected" security best practices. The architecture adopts a **Zero-Trust Origin** model, ensuring the S3 storage layer is never publicly exposed and all traffic is strictly routed through the secure CDN layer.

## 🔒 Implemented Security Measures

### 1. S3 Block Public Access
* **Implementation:** "Block all public access" is enabled at the bucket level.
* **Effect:** Prevents any direct access to objects via standard S3 URLs. The bucket is completely isolated from the public internet.

### 2. Origin Access Control (OAC)
* **Implementation:** CloudFront communicates with S3 using AWS Signature Version 4 (SigV4) via Origin Access Control.
* **Effect:** A strict Bucket Policy ensures that only the specific CloudFront distribution (authenticated via OAC) can read data. Unauthorized services or users are instantly denied.

### 3. HTTPS Enforcement
* **Implementation:** The CloudFront Viewer Protocol Policy is set to **"Redirect HTTP to HTTPS"**.
* **Effect:** Ensures all data is encrypted in transit using TLS 1.2/1.3, protecting against man-in-the-middle attacks.

### 4. Restricted HTTP Methods
* **Implementation:** The CloudFront behavior is configured to allow only **GET** and **HEAD** methods.
* **Effect:** Prevents any modification of the server content via public endpoints (blocks PUT, POST, DELETE, PATCH).

### 5. Identity & Access Management (IAM)
* **Implementation:** No long-term IAM access keys or secrets are stored in the repository.
* **Effect:** Access is managed entirely through AWS Service Principals and temporary permissions, eliminating the risk of credential leakage.

### 6. Availability & Integrity
* **Implementation:** Manual cache invalidation is performed only during deployments.
* **Effect:** Prevents stale content delivery and ensures users always receive the latest verified version of the site.

## ⚠️ Threat Model & Mitigation

| Threat Scenario | Mitigation Strategy | Result |
| :--- | :--- | :--- |
| **Public Bucket Exposure** | Enabled "Block Public Access" on S3 | Attack surface removed |
| **Data Interception** | Enforced HTTPS (TLS) Redirects | Encrypted traffic |
| **Bypass of CDN** | Origin Access Control (OAC) | Direct S3 access blocked (403 Forbidden) |
| **Data Deletion/Overwrites** | Read-Only Methods (GET/HEAD) | Write operations rejected |
| **Cost Abuse (DDoS)** | CloudFront Caching & Geo-Restrictions | Origin protected from traffic spikes |

## ✅ Conclusion
This security architecture provides a production-ready environment for static hosting. By decoupling the storage layer from the delivery layer and enforcing strict access controls, the solution minimizes risk while maximizing availability.