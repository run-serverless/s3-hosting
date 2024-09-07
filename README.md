# S3 Hosting Setup

Deploy infrastructure to host a static website on AWS S3. Includes setting up:

- S3 bucket to host the website
- CloudFront (CDN) distribution to serve the website
- SSL certificate for the website
- Everything configured using custom domain name

Domain name must be registered and managed in Route 53.

## Prerequisites

- AWS account
- Domain name registered in Route 53 with a Hosted Zone
- AWS CLI installed and configured with credentials
- A centralised Serverless Framework deployment bucket using the format `<aws-account-id>--serverless-deploys`

Replace `<aws-account-id>` with your AWS account ID.

## Usage

### Deploy Infrastructure

```bash
npx serverless deploy --param="domain=<domain-name>"
```

- Replace `<domain-name>` with the domain name, i.e. `my-project.com`

**Note:** The SSL certificate requires manual validation via DNS. This must be done via the AWS Console in the
Certificate Manager in N. Virginia (us-east-1) region. Follow the instructions to add CNAME records to the domain.
Deployment will pause until the certificate is validated. This might take 5 minutes or more.

Do this when the CLI shows:

```bash
Creating CloudFormation stack (2/4)
```

### Remove Infrastructure

```bash
serverless remove
```

**Warning:** This will remove all resources created by the project and take down your website.
