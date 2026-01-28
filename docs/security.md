\# Security



\## Security Overview

This project focuses on secure delivery of static website content using AWS best practices. The architecture ensures that the S3 bucket is never publicly exposed and that all traffic is served securely via CloudFront.



\## Implemented Security Measures



\### 1. S3 Block Public Access

\- Public access is blocked at the bucket level.

\- Prevents direct access to objects via S3 URLs.



\### 2. Origin Access Control (OAC)

\- CloudFront accesses S3 using Origin Access Control.

\- Bucket policy allows access only from the specific CloudFront distribution.

\- Prevents unauthorized services or users from accessing the bucket.



\### 3. HTTPS Enforcement

\- CloudFront viewer protocol policy redirects HTTP to HTTPS.

\- Ensures all data is encrypted in transit.



\### 4. Limited HTTP Methods

\- Only GET and HEAD methods are allowed.

\- Prevents misuse of POST, PUT, DELETE, and PATCH methods.



\### 5. No Credential Exposure

\- No IAM access keys or secrets are stored in the repository.

\- All access is controlled via AWS managed services and policies.



\### 6. Cache Invalidation Control

\- Manual invalidation is used when content changes.

\- Prevents stale or incorrect content from being served.



\### 7. Cost and Abuse Protection

\- Architecture minimizes risk of abuse by:

&nbsp; - Blocking direct S3 access

&nbsp; - Limiting allowed methods

&nbsp; - Using CloudFront caching



\## Threat Model



| Threat | Mitigation |

|--------|------------|

| Public bucket access | Block Public Access enabled |

| Data interception | HTTPS enforced |

| Unauthorized access | OAC + bucket policy |

| Accidental data deletion | Versioning + lifecycle rules |

| Cost abuse | CDN caching + private bucket |



\## Conclusion

This setup follows industry best practices for hosting static websites securely on AWS and is suitable for production-level workloads.



