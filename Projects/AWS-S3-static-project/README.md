# 🪣 Project 01 — AWS S3 Static Website

> **Services:** Amazon S3 | **Status:** ✅ Complete

---

## 🎯 Project Overview

Host a fully functional **static website** on AWS using **Amazon S3** static website hosting. Configure bucket policies to allow public access, upload HTML/CSS assets, and verify the live site via the S3 website endpoint.

---

## 📚 What I Did

### Steps Completed

| Step | Action | Screenshot |
|---|---|---|
| 1 | Created an S3 bucket | `step-1-create-s3-bucket.png` |
| 2 | Accessed the bucket settings | `step-2-access-bucket.png` |
| 3 | Enabled public access | `step-3-enable-public-access.png` |
| 4 | Applied a bucket policy | `step-4-bucket-policy.png` |
| 5 | Enabled static website hosting | `step-5-static-website-hosting.png` |
| 6 | Verified the website is live | `step-6-website-live.png` |

---

## 🧠 Key Concepts Covered

### S3 Static Website Hosting
S3 can serve HTML, CSS, and JavaScript files directly as a website — no EC2 server needed.

**Endpoint format:**
```
http://bucket-name.s3-website-region.amazonaws.com
```

### Bucket Policy for Public Access
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```
- `Principal: "*"` — anyone on the internet
- `s3:GetObject` — read-only (can't upload or delete)
- Resource ends in `/*` — applies to all objects in the bucket

### Block Public Access Settings
By default, S3 blocks all public access. To host a public website:
1. Uncheck "Block all public access"
2. Acknowledge the warning
3. Then apply the bucket policy above

### Index & Error Documents
```
Index document: index.html   ← Loaded when visiting the root URL
Error document: error.html   ← Shown for 404 errors
```

---

## 💡 Key Takeaways

1. **S3 websites are HTTP only** — for HTTPS, put CloudFront in front with an ACM certificate.
2. **Block public access is on by default** — you must explicitly disable it for public websites.
3. **S3 website hosting vs S3 object URL** — the website endpoint handles `index.html` routing; the object URL doesn't.
4. **Bucket names must be globally unique** — and for website hosting, the name must match your domain if using Route 53.
5. **Cost is minimal** — static sites on S3 cost pennies per month for low-traffic sites.

---

## 📸 Screenshots

> Screenshots available in [`./aws-hybrid-cloud-solution-cafe/images/`](./aws-hybrid-cloud-solution-cafe/images/)
