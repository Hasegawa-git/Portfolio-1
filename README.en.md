# Static Website Hosting with S3 + CloudFront + Route 53

## ✅ Deployed Site   
URL：https://www.takahiro-hasegawa.net

## ✅ AWS Services Used  
- Amazon S3 (Static Website Hosting)  
- Amazon CloudFront (CDN + HTTPS)  
- Amazon Route 53 (DNS)  
- AWS Certificate Manager (SSL Certificate)

## ✅ Overview  
This project demonstrates how to host a static website using a custom domain (`www.takahiro-hasegawa.net`) with full HTTPS support by combining multiple AWS services.  
The `index.html` file hosted in S3 is delivered via CloudFront, DNS routing is handled by Route 53, and HTTPS is enabled through ACM.

## ✅ Architecture Diagram  
```mermaid
flowchart TD
    User["User"]
    DNS["Route 53\n(DNS Routing)"]
    CF["CloudFront\n(CDN + HTTPS)"]
    S3["S3 Bucket\n(index.html)"]
    ACM["AWS Certificate Manager\n(SSL Certificate)"]

    User -->|"① Access / DNS Resolution"| DNS
    DNS -->|"② Redirect to CloudFront"| CF
    CF -->|"③ Fetch index.html"| S3
    CF -->|"④ Return HTTPS Response"| User
    ACM -->|"Provide SSL Certificate"| CF
```
## ✅ Service Configuration Details

### 1. Route 53 (A Record)
Configured DNS routing from `www.takahiro-hasegawa.net` to the CloudFront distribution.

![Route 53 A Record](screenshots/route53-a-record.png)

### 2. CloudFront General Settings (HTTPS & Alternate Domain)
Set up a custom domain and applied an SSL certificate from AWS Certificate Manager.

![CloudFront General Settings](screenshots/cloudfront-general.png)

### 3. CloudFront Origin Settings (S3 Integration)
Defined the origin of the distribution as an S3 bucket hosting the static content.

![CloudFront Origin Settings](screenshots/cloudfront-origin.png)

### 4. SSL Certificate (ACM)
Issued in the N. Virginia (`us-east-1`) region and validated via CNAME record.

![ACM Certificate Details](screenshots/acm-certificate.png)

### 5. S3 Object: index.html
Uploaded and stored `index.html` as the main content of the website.

![S3 index.html Details](screenshots/s3-index-html.png)

### 6. S3 Static Website Hosting
Enabled static website hosting from the S3 bucket's properties.

![S3 Static Hosting Settings](screenshots/s3-static-hosting.png)

### 7. Final Website Display
Verified HTTPS access to the website via CloudFront using the custom domain.

![Final Website Display](screenshots/final-site.png)

## ✅ Key Learnings
- Integration between AWS services (S3 / CloudFront / Route 53 / ACM)
- Understanding of DNS, SSL certificate issuance, CNAME validation, and HTTPS
- Behavior and importance of cache control and CDN
- Troubleshooting and resolving issues independently during deployment

## ✅ Notes
The HTML content itself is intentionally simple—this project focuses on designing and deploying the AWS infrastructure.
