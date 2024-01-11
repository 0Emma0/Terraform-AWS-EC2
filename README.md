In this repo, we will describe how to create an EC2 instance on Amazon Web Services using Terraform.

# Prerequisites
To create an EC2 instance on AWS with Terraform, we will need the following prerequisites in place:

## Terraform installed: 
You will need to have Terraform installed on your machine to write and execute Terraform code. If you don't have Terraform installed, you can visit the official site. https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli 

## AWS Account: 
You will need an active AWS account where you will create the resources on AWS, if you don't have an AWS account yet, you can create one from here: https://aws.amazon.com/free

## Create an IAM User on AWS:
Create a new IAM user with programmatic access, which will be used by Terraform to create resources on AWS. You will use the key ID, secret access key, and default region in the next steps. Save all this information to be used on the "aws configure" command. 

[How to create an IAM User ](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)

## AWS CLI installed:
You must have the AWS Command Line Interface (CLI) installed on your machine to interact with EC2 instances and other AWS resources from the command line. You can download the appropriate version for your system here: https://aws.amazon.com/cli/

## AWS CLI Configuration: 
Once you have installed the AWS CLI, you can configure it by running the following command:
```
aws configure
```
This will prompt you to enter your AWS access key ID, secret access key, default region, and default output format. You can get your access key ID and secret access key from the AWS Management Console by navigating to IAM > Users.

If you have not already done so, you should create an IAM user with the minimum required permissions necessary.

## Authentication with AWS:
To use your IAM credentials to authenticate the Terraform AWS provider, set the AWS_ACCESS_KEY_ID environment variable.
```
export AWS_ACCESS_KEY_ID=
```
Now, set your secret key.
```
export AWS_SECRET_ACCESS_KEY=
```
 

If you don't have access to IAM user credentials, use another authentication method described in the AWS provider documentation.

# How to create an EC2 instance using Terraform
Once you have completed all prerequisites you can create the EC2 Instance with the next steps:

1- Clone this repo and go to the directory that contains the main.tf configuration file.

2- Initialize the Terraform directory by running the below command:
```
terraform init
```
3- You can also make sure your configuration is syntactically valid and internally consistent by using the terraform validate command.
```
terraform validate
```
4- Run terraform plan. Terraform will create an execution plan.
```
terraform plan
```
5- Run terraform apply and enter yes to confirm the execution. (This step will create the EC2 Instance on AWS)
```
terraform apply
```
Navigate the AWS portal, go to EC2 section on us-west-2 region, and view your EC2 instance created using Terraform.

To avoid being charged, you can destroy the EC2 instance with terraform destroy.
```
terraform destroy
```

