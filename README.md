# Static Website Deployment on AWS using S3, CloudFront & GitHub Actions

## 📌 Project Overview

_This project demonstrates how to deploy a static website on Amazon Web Services (AWS) using Amazon S3 for hosting, Amazon CloudFront as a Content Delivery Network (CDN), and GitHub Actions to automate deployment through a CI/CD pipeline._  
_Whenever changes are pushed to the GitHub repository, GitHub Actions automatically uploads the updated website files to the S3 bucket and invalidates the CloudFront cache, making the latest version available immediately._

---

## 🚀 Architecture
```text
Developer
     │
     │ git push
     ▼
 GitHub Repository
     │
     ▼
 GitHub Actions (CI/CD)
     │
     ├────────────► Upload files to Amazon S3
     │
     └────────────► Create CloudFront Invalidation
                          │
                          ▼
                   Amazon CloudFront
                          │
                          ▼
                     End Users
```

## 🛠️ Technologies Used

| Technology          | Purpose / Usage                                                                                                      |
| ------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **AWS S3**          | Hosts the static website files (HTML, CSS, JavaScript).                                                              |
| **AWS CloudFront**  | Delivers website content globally with low latency and caches files for faster performance.                          |
| **AWS IAM**         | Manages secure access by creating a deployment user with least-privilege permissions.                                |
| **GitHub**          | Stores the project source code and tracks version history.                                                           |
| **GitHub Actions**  | Automates the CI/CD pipeline by deploying website updates to S3 and invalidating the CloudFront cache on every push. |
| **YAML**            | Defines the GitHub Actions workflow configuration (`deploy.yml`).                                                    |
| **HTML**            | Creates the structure and content of the static website.                                                             |
| **CSS**             | Styles the website and controls its layout and appearance.                                                           |
| **JavaScript (JS)** | Adds interactivity and dynamic behavior to the website.                                                              |


## 📁 Project Structure

```text
project-name/
│
├── frontend/
│   └── index.html
│
└── .github/
    └── workflows/
        └── deploy.yml
```

## ⚙️ AWS Configuration

Step 1: Create S3 Bucket
* Create a new S3 bucket
* Block all public access
* Enable Static Website Hosting
* Set index.html as the default document.
* Upload the website files to the bucket.

Step 2: Configure CloudFront
* Create a CloudFront Distribution
* Select the S3 bucket as the origin
* Create an Origin Access Control (OAC)
* Attach the OAC to the distribution
* Deploy the distribution

After deployment, use the CloudFront Domain Name to access the website.

Step 3: Create IAM User
* Create an IAM user: `github-s3-cloudfront-deployer`
* Attach the following permissions:

  **Amazon S3**
  * `ListBucket`
  * `GetObject`
  * `PutObject`
  * `DeleteObject`

  **Amazon CloudFront**
  * `CreateInvalidation`
* Generate:
    * Access Key ID
    * Secret Access Key

## 🔐 GitHub Secrets

Add the following secrets to your GitHub repository:

| Secret Name                | Description                |
| -------------------------- | -------------------------- |
| AWS_ACCESS_KEY_ID          | IAM User Access Key        |
| AWS_SECRET_ACCESS_KEY      | IAM User Secret Key        |
| AWS_REGION                 | AWS Region                 |
| S3_BUCKET                  | S3 Bucket Name             |
| CLOUDFRONT_DISTRIBUTION_ID | CloudFront Distribution ID |


## ⚡ GitHub Actions Workflow

The workflow performs the following tasks automatically:  
- Checkout repository
- Configure AWS credentials
- Upload website files to S3
- Invalidate CloudFront cache
- Deploy the latest website version

## 🔄 Deployment Process
1. Clone the repository.  
 `git clone <repository-url>`

2. Make changes inside the `frontend` folder.
3. Commit the changes.  
`git add .`  
`git commit -m "Updated website"`
4. Push to GitHub.  
`git push origin main`  

5. GitHub Actions automatically:
- Uploads files to Amazon S3
- Invalidates the CloudFront cache
- Publishes the latest website

No manual deployment is required.

## ✅ Features
- Static website hosting on Amazon S3
- Private S3 bucket using Origin Access Control (OAC)
- Global content delivery with CloudFront
- Automated deployment using GitHub Actions
- Secure AWS authentication using GitHub Secrets
- Automatic CloudFront cache invalidation
- Fully automated CI/CD pipeline

## 📖 What I Learned
- Hosting static websites using Amazon S3
- Configuring CloudFront for secure content delivery
- Managing AWS permissions with IAM
- Creating GitHub Secrets for secure credential management
- Writing GitHub Actions workflows
- Building an automated CI/CD pipeline
- Deploying website updates automatically with GitHub

## 🎯 Outcome

Successfully built and deployed a static website using AWS services with an automated CI/CD pipeline. Any change pushed to the GitHub repository is automatically deployed to Amazon S3, and CloudFront cache invalidation ensures users always see the latest version of the website.