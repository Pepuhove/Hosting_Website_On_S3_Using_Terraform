# Hosting_Website_On_S3_Using_Terraform
Hosting a simple website on amazon s3 using terraform (IaC)
This project demonstrates how to host a simple static website on Amazon S3 using Terraform as Infrastructure as Code (IaC).
The website consists of HTML and CSS files, which are deployed to an S3 bucket.

https://github.com/Pepuhove/Hosting_Website_On_S3_Using_Terraform/blob/9fb8348aa459b4488760e7642147d4a9d698d7e6/website%20on%20s3.png

# Prerequisites

Before you begin, ensure you have the following:

Terraform installed (Install Terraform)

AWS CLI configured with necessary credentials (Install AWS CLI)

An AWS account with appropriate permissions

# Project Structure

Hosting_Website_On_S3_Using_Terraform/

├── main.tf

├── variables.tf

├── outputs.tf

├── index.html

├── styles.css

└── README.md

# Terraform Configuration

1. Define the S3 Bucket

Terraform provisions an S3 bucket to store and serve the static website content.

resource "aws_s3_bucket" "website_bucket" {
  bucket = var.bucket_name
  acl    = "public-read"

  website {
    index_document = "index.html"
    error_document = "index.html"
  }
}

2. Upload Website Files

Terraform will upload the index.html and styles.css files to the S3 bucket.

resource "aws_s3_object" "index_html" {
  bucket = aws_s3_bucket.website_bucket.id
  key    = "index.html"
  source = "index.html"
  content_type = "text/html"
}

resource "aws_s3_object" "styles_css" {
  bucket = aws_s3_bucket.website_bucket.id
  key    = "styles.css"
  source = "styles.css"
  content_type = "text/css"
}

3. Output the Website URL

Terraform provides the website endpoint as an output.

output "website_url" {
  value = aws_s3_bucket.website_bucket.website_endpoint
}

# Usage

1. Initialize Terraform

Run the following command to initialize the working directory:

terraform init

2. Plan the Deployment

Generate and review the execution plan:

terraform plan

3. Apply the Configuration

Deploy the infrastructure:

terraform apply -auto-approve

4. Access the Website

Once the deployment is complete, Terraform will output the S3 website URL. Open it in your browser to view the hosted site.

# Cleanup

To delete the resources created by Terraform, run:

terraform destroy -auto-approve

# Conclusion

This project showcases how to use Terraform to automate the deployment of a static website on Amazon S3.
By leveraging Terraform's declarative approach, infrastructure provisioning becomes efficient, repeatable, and manageable.

