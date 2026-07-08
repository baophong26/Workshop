---
title: "Configuring Route 53 and SSL"
date: 2024-01-01
weight: 12
chapter: false
pre: " <b> 5.12. </b> "
---

#### Introduction

This section guides you through configuring a custom domain with HTTPS for ITCoach. You will:
- Purchase a domain (e.g., itcoach24h.xyz)
- Create an SSL certificate with ACM
- Configure Route 53 DNS
- Attach the domain to CloudFront


#### Step 1: Purchase Domain (Namecheap)

**1. Visit Namecheap.com**
- Search for the domain you want (e.g., `itcoach24h.xyz`)
- Add to cart

**2. Checkout**
- Disable "I'm registering on behalf of a company"
- Keep **Free Domain Privacy** enabled ✅
- Uncheck **Auto-renew** (to avoid automatic renewal)
- Pay with international credit card

#### Step 2: Create Hosted Zone on Route 53

**1. Create Hosted Zone**
- Search for **Route 53** → **Hosted zones** → **Create hosted zone**
- Domain name: `itcoach24h.xyz`
- Type: **Public hosted zone**
- **Create hosted zone**

![Create Hosted Zone](/images/5-Workshop/5.12-route53/001-route53-hosted-zone.png)

**2. Get NS Records**
- After creation, you'll see 4 **NS records**
- Copy the 4 nameservers (format: `ns-xxx.awsdns-xx.com`)

**3. Update Nameservers on Namecheap**
- Go to Namecheap → Dashboard → manage domain
- **Nameservers** → select **Custom DNS**
- Paste the 4 nameservers from Route 53
- **Save**

![Update Nameservers](/images/5-Workshop/5.12-route53/002-namecheap-custom-dns.png)


#### Step 3: Request SSL Certificate (ACM)


**1. Switch Region**
- Top right corner of AWS Console → switch region to **us-east-1**

**2. Request Certificate**
- Search for **Certificate Manager (ACM)**
- **Request a certificate** → **Next**

**3. Configure Certificate**
- Fully qualified domain name:
  - Domain 1: `itcoach24h.xyz`
  - Click **Add another name** → Domain 2: `*.itcoach24h.xyz`
- Validation method: **DNS validation**
- **Request**

![Request Certificate](/images/5-Workshop/5.12-route53/003-acm-request-cert.png)

**4. Validate Certificate**
- Click on the certificate (status *Pending validation*)
- **Domains** tab → **Create records in Route 53**
- **Create records**

Wait 3-5 minutes → Status changes to **Issued** (green) ✅

#### Step 4: Attach Domain to CloudFront


**1. Edit CloudFront Distribution**
- **CloudFront** → click distribution `itcoach-distribution`
- **General** tab → **Edit**

**2. Add Alternate Domain Names**
- **Alternate domain names (CNAMEs)** → **Add item**
  - Add: `itcoach24h.xyz`
  - Add: `www.itcoach24h.xyz`

**3. Select SSL Certificate**
- **Custom SSL certificate** → select the certificate you just created
- **Save changes**

![CloudFront Custom Domain](/images/5-Workshop/5.12-route53/004-cloudfront-custom-domain.png)

#### Step 5: Create DNS Records

**1. Create A Record for Root Domain**
- **Route 53** → **Hosted zones** → click `itcoach24h.xyz`
- **Create record**
  - Record name: *(leave empty)*
  - Record type: **A**
  - Enable **Alias** toggle ✅
  - Route traffic to: **Alias to CloudFront distribution**
  - Select your distribution
  - **Create records**

**2. Create A Record for www**
- **Create record**
  - Record name: `www`
  - Record type: **A**
  - Enable **Alias** toggle ✅
  - Route traffic to: **Alias to CloudFront distribution**
  - Select your distribution
  - **Create records**

![DNS Records](/images/5-Workshop/5.12-route53/005-route53-alias-record.png)

#### Step 6: Test Domain

Visit the domain in your browser:
```
https://itcoach24h.xyz
https://www.itcoach24h.xyz
```

Check the SSL certificate by clicking the lock icon in the address bar.

#### Result

✅ Custom domain with HTTPS is now working!

#### Information to Save

```
Domain: itcoach24h.xyz
SSL Certificate: ACM us-east-1 (Issued)
Nameservers: AWS Route 53
CloudFront CNAMEs: itcoach24h.xyz, www.itcoach24h.xyz
DNS Records: A records (Alias to CloudFront)
```

#### Estimated Cost

- .xyz Domain: ~$1-2/year (Namecheap)
- Route 53 Hosted Zone: $0.50/month
- ACM Certificate: **FREE**
- DNS Queries: $0.40/million queries

**Total: ~$0.50/month + $2/year domain**

#### Next Steps

Move to the next section to set up Monitoring with CloudWatch.
