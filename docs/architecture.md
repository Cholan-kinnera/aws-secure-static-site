🏗️ System Architecture
📌 Overview
This project implements a serverless, secure, and scalable architecture for static website hosting. By leveraging Amazon CloudFront as a Content Delivery Network (CDN) and Amazon S3 as a private origin, the design ensures high performance, global availability, and robust security.

The core principle of this architecture is "Zero-Trust Origin," meaning the storage layer (S3) is completely isolated from the public internet and only accepts authenticated requests from the specific CloudFront distribution.

📐 Architecture Diagram
Logical Flow
graph LR
    User(User Browser) -- HTTPS/TLS --> CF(Amazon CloudFront)
    CF -- Origin Access Control --> S3(Private Amazon S3 Bucket)
    
    subgraph "Public Internet"
    User
    end
    
    subgraph "AWS Cloud"
    CF
    S3
    end
    
    style S3 fill:#E76F51,stroke:#333,stroke-width:2px,color:white
    style CF fill:#2A9D8F,stroke:#333,stroke-width:2px,color:white
    (For a high-resolution visual diagram, please refer to the diagram/ folder or the PDF documentation in docs/.)

🔄 Request Flow
User Request: The user navigates to the website domain via a browser. The request is routed to the nearest CloudFront Edge Location to minimize latency.

HTTPS Enforcement: CloudFront strictly accepts HTTPS traffic. Any HTTP requests are automatically redirected to HTTPS (Status Code 301).

Edge Caching: CloudFront checks its cache.

Cache Hit: Content is returned immediately to the user.

Cache Miss: CloudFront forwards the request to the origin (S3).

Origin Authentication: CloudFront signs the request using Origin Access Control (OAC) to prove its identity.

Private S3 Access: The S3 Bucket Policy validates the OAC signature. If valid, S3 returns the requested file to CloudFront.

Response: CloudFront caches the file for future requests and serves it to the user.
Component,AWS Service,Configuration Highlights
Storage (Origin),Amazon S3,• Block All Public Access: Enabled (100% Private).• Bucket Policy: Allows s3:GetObject only from CloudFront Service Principal.• Versioning: Enabled for recovery.
Delivery (CDN),Amazon CloudFront,• Protocol: HTTPS Only (Redirect HTTP).• Access Control: Origin Access Control (OAC).• Caching: Optimized Policy (CachingOptimized).• Price Class: Use all edge locations.
Security,IAM & Policies,• Least Privilege access controls.• No AWS credentials stored in the codebase.
🔐 Security & Optimization Features
🛡️ Security Implementation
Private Origin: Direct public access to the S3 bucket URL is strictly blocked. Users cannot bypass the CDN.

Origin Access Control (OAC): Utilizes AWS Signature Version 4 (SigV4) for secure, authenticated communication between CloudFront and S3.

Encryption in Transit: All data is transmitted via TLS 1.2/1.3.

💰 Cost Optimization
Lifecycle Rules: Configured to automatically expire non-current object versions after 30 days to prevent storage bloat.

Caching Strategy: High Time-To-Live (TTL) settings in CloudFront reduce the number of read requests sent to S3, lowering operation costs.

Free Tier Friendly: Designed to operate within the AWS Free Tier limits (5GB S3 Storage, 1TB CloudFront transfer).

🏆 Key Benefits
✅ High Security: Attack surface is minimized by hiding the origin server.

✅ Global Performance: Content is served from Edge Locations closest to the user.

✅ Scalability: Serverless architecture handles traffic spikes without manual intervention.

✅ Maintainability: No servers to patch or manage (EC2-free).