# AWS S3 & CloudFront Automated CI/CD Pipeline

In this project, I built and automated the deployment of a static website to **AWS S3** and **Amazon CloudFront** using a **GitHub Actions** CI/CD pipeline.

---

## 🛠️ What I Did (Step-by-Step)

### Step 1: Created the AWS S3 Bucket
1. I logged into the **AWS Management Console** and navigated to **Amazon S3**.
2. I created a new bucket named `static-web-910965284133-eu-west-1` in the `eu-west-1` region.
3. I kept **Block all public access** enabled to enforce security best practices.

***Documentation & References:***
- [*AWS S3 Console Documentation*](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html)
- [*S3 Block Public Access Settings*](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html)

---

### Step 2: Set Up IAM User & Credentials
1. I navigated to the **IAM** service in AWS and created a dedicated user named `github-actions-s3`.
2. I attached the `AmazonS3FullAccess` policy directly to grant the necessary upload permissions.
3. I generated long-term **Access Keys (CLI)** for this user and copied the `Access Key ID` and `Secret Access Key`.

***Documentation & References:***
- [*Creating IAM Users in AWS*](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)
- [*Managing Access Keys for IAM Users*](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)

---

### Step 3: Configured GitHub Repository Secrets
1. In my GitHub repository, I navigated to **Settings** ➡️ **Secrets and variables** ➡️ **Actions**.
2. I created two repository secrets to store my credentials securely:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`

***Documentation & References:***
- [*Encrypted Secrets in GitHub Actions*](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

---

### Step 4: Configured CloudFront & Origin Access Control (OAC)
1. I navigated to **Amazon CloudFront** and created a new distribution targeting my S3 bucket origin.
2. I enabled **Origin Access Control (OAC)** so that S3 content is served securely through CloudFront only.
3. I copied the generated **Bucket Policy** and updated my S3 bucket permissions to grant CloudFront `s3:GetObject` access.

***Documentation & References:***
- [*Amazon CloudFront Developer Guide*](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
- [*Restricting Access to S3 Origins Using OAC*](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html)

---

### Step 5: Built the GitHub Actions CI/CD Pipeline
1. I created a workflow file at `.github/workflows/deploy.yml`.
2. I configured the pipeline to run automatically on every `push` to the `main` branch.
3. I used `aws s3 sync .` to deploy changed files efficiently and added `aws cloudfront create-invalidation` to clear the cache instantly.

***Documentation & References:***
- [*Configuring AWS Credentials Action*](https://github.com/aws-actions/configure-aws-credentials)
- [*AWS CLI S3 Sync Command*](https://docs.aws.amazon.com/cli/latest/reference/s3/sync.html)
- [*CloudFront Cache Invalidation*](https://docs.aws.amazon.com/cli/latest/reference/cloudfront/create-invalidation.html)

---

## How to Run & Test

1. I make changes to my project files locally.
2. I push my changes to GitHub:
   git add .
   git commit -m "Updated site content"
   git push origin main
3. Visit: https://d1r1nkvg0lvtb9.cloudfront.net   