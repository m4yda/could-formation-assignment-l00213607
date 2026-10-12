# AWS S3 & CloudFront Automated CI/CD Pipeline L00213607
Automated deployment of a static website to **AWS S3** and **Amazon CloudFront** using **GitHub Actions**.

# Website Link: https://d1r1nkvg0lvtb9.cloudfront.net
---

## Setup & Steps

### 1. AWS S3 Bucket Creation
- Created an S3 bucket named `static-web-910965284133-eu-west-1` in `eu-west-1`.
- Kept **Block all public access** enabled for security.
- *Ref:* [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html)

### 2. IAM User & Permissions
- Created an IAM user named `github-actions-s3`.
- Attached the `AmazonS3FullAccess` policy.
- Generated CLI Access Keys (`Access Key ID` and `Secret Access Key`).
- *Ref:* [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)

### 3. GitHub Secrets
- Stored credentials in GitHub Repository Secrets (`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`).
- *Ref:* [GitHub Actions Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

### 4. CloudFront & OAC Setup
- Created a CloudFront distribution linked to the S3 bucket.
- Enabled Origin Access Control (OAC).
- Applied the generated S3 Bucket Policy for `s3:GetObject` access.
- *Ref:* [Amazon CloudFront OAC Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html)

### 5. GitHub Actions Workflow
- Created `.github/workflows/deploy.yml` triggered on push to `main`.
- Used `aws s3 sync .` to update modified files.
- Added `aws cloudfront create-invalidation` to clear cache instantly.
- *Ref:* [AWS CLI S3 Sync](https://docs.aws.amazon.com/cli/latest/reference/s3/sync.html)

---

## Deployment & Testing

1. Make changes locally.
2. Push to main:
   ```bash
   git add .
   git commit -m "Updated website"
   git push origin main