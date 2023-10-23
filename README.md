# AWS Cloud Resume

This is the end result of my take on the [Cloud Resume Challenge](https://cloudresumechallenge.dev/) - a multiple step resume project that tasks the user with developing and deploying a website running on a serverless cloud infrastructure.

## [Link to page](https://resume.jsebs.io)

## Architecture

![project architecture](https://github.com/jsebs/cloud_resume/blob/main/website/images/cloud_res_arch.jpg)

* The front end of the page is written in HTML/CSS (obviously) along with some JavaScript/jQuery to add functionality/animations, and is continuously deployed to an S3 bucket and served by the CloudFront CDN. 

* DNS routing was set up with Route 53 to point a custom domain to keep the URL nice and simple instead of using the jibberish that CloudFront provides as their standard Distribution Domain Names (ex. adsf834jkl3209f2.cloudfront.net).

* A REST API is created using a Lambda function (Python boto3) to retrieve, display, and update an item from a DynamoDB table on our page which is implemented as a view counter.

* Provisioning of the front end is automated using a CI/CD pipeline that runs on GitHub actions deploying updates to the S3 bucket and CloudFront.

* Provisioning of the back end is handled using Terraform to push updates to the Lambda function, DynamoDB table, and their policies. 

### List of Services Used

* S3
* CloudFront
* Certificate Manager
* Lambda (Python)
* Dynamo DB
* GitHub + GitHub Actions
* Terraform
