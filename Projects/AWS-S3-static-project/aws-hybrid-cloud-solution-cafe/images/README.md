# ☕ AWS S3 Static Website Setup: Our Freshly Ground Cafe

## **Step 1: Create the S3 Bucket**
**Action:** In AWS Console S3 section, entered bucket name:
- **Bucket Name:** `ourfreshlygroundcafe2026`
- **Note:** Public access was blocked by default
- **Action:** Left all settings as default, scrolled down, clicked **"Create bucket"**

![Create S3 Bucket](images/step-1-create-s3-bucket.png)

---

## **Step 2: Access Bucket Settings**
**Action:** After creation, clicked on the bucket name `ourfreshlygroundcafe2026`

![Access Bucket](images/step-2-access-bucket.png)

---

## **Step 3: Enable Public Access**
**Action:** Under **Permissions** → **Block public access**
- **Action:** Disabled **"Block all public access"**
- **Action:** Saved changes

![Enable Public Access](images/step-3-enable-public-access.png)

---

## **Step 4: Configure Bucket Policy**
**Action:** Scrolled down to **Bucket policy** section
- **Action:** Clicked **"Edit"** to add a policy
- **Action:** Added the required public read policy
- **Action:** Saved changes

![Configure Bucket Policy](images/step-4-bucket-policy.png)

---

## **Step 5: Enable Static Website Hosting**
**Action:** Navigated to **Properties** → **Static website hosting**
- **Action:** Clicked **"Edit"**
- **Action:** Enabled static website hosting
- **Action:** Added `index.html` as index document
- **Action:** Saved changes

![Enable Static Website Hosting](images/step-5-static-website-hosting.png)

---

## **✅ Step 6: Website Live!**
**Result:** After configuration, the static website was accessible via S3 endpoint URL

![Website Live](images/step-6-website-live.png)

---

