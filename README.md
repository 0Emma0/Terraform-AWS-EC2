In this repo, we will describe how to create an EC2 instance on Amazon Web Services using Terraform.

# Prerequisites
To create an EC2 instance on AWS with Terraform, we will need the following prerequisites in place:

## AWS Account: 
The first prerequisite you need to have is an active AWS account where you will create the resources on AWS, if you don't have an AWS account yet, you can create one from here: https://aws.amazon.com/free

## Create an IAM User on AWS:
Create a new IAM user with programmatic access, which will be used by Terraform to create resources on AWS. You will use the key ID, secret access key, and default region in the next steps. Save all this information to be used on the "aws configure" command. 

[How to create an IAM User ](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)

## Terraform installed: 
You will need to have Terraform installed on your machine to write and execute Terraform code. If you don't have Terraform installed, you can visit the official site. https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli 

## AWS CLI installed:
You must have the AWS Command Line Interface (CLI) installed on your machine to interact with EC2 instances and other AWS resources from the command line. You can download the appropriate version for your system here: https://aws.amazon.com/cli/

## AWS CLI Configuration: 
Once you have installed the AWS CLI, you can configure it by running the following command:
```
aws configure
```
This will prompt you to enter your AWS access key ID, secret access key, default region, and default output format. You can get your access key ID and secret access key from the AWS Management Console by navigating to IAM > Users.

If you have not already done so, you should create an IAM user with the minimum required permissions necessary.

## EC2 Instance SSH:
SSH key pair: To access a Linux-based EC2 instance via SSH, you will need an SSH key pair.
Run the following command to generate a new SSH key pair:
```
ssh-keygen -t rsa -b 4096
```
This will create a new RSA key pair with a length of 4096 bits.

You will be prompted to enter a file name to save the key pair. The default location is in your user’s home directory under the .ssh directory. You can choose a different file name or directory if you prefer.

You will be prompted to enter a passphrase for the key pair. This is optional but recommended to add an extra layer of security.

The ssh-keygen command will generate two files: a private key file and a public key file. The private key file should be kept secure and never shared with anyone. The public key file can be shared with Amazon EC2 instances to allow SSH access.

Finally, to use the key pair with an Amazon EC2 instance, you must add the public key to the instance when you configure it with Terraform.

## Authentication with AWS:
You can configure Terraform to authenticate with AWS using several methods. With AWS CLI installed, we can use the named profiles method, which is a recommended approach for authenticating Terraform to AWS because it allows you to manage multiple sets of AWS credentials and control access to resources using IAM roles and policies.

First, ensure the AWS CLI is installed and configured using the guidelines in the prerequisite section to add the AWS access key ID and secret access key using the aws configure command. By default, the AWS CLI-named profiles use the same access key ID and secret access key as your default profile, so you don’t need to specify them again for different profiles.

Create an AWS CLI named profile for Terraform in the ~/.aws/config file (Linux and macOS) or %UserProfile%\.aws\config file (Windows). You can override the default access key ID and secret access key for a named profile by setting the aws_access_key_id and aws_secret_access_key attributes if required.

# How to create an EC2 instance using Terraform
Once you have completed all prerequisites you can create the EC2 Instance with the next steps:

1- Clone this repo and go to the directory that contains the main.tf configuration file.

2- Initialize the Terraform directory by running the below command:
```
terraform init
```
3- Run terraform plan. Terraform will create an execution plan.
```
terraform plan
```
4- Run terraform apply and enter yes to confirm the execution. (This step will create the EC2 Instance on AWS)
```
terraform apply
```
Navigate the AWS portal, go to EC2 section on us-west-2 region, and view your EC2 instance created using Terraform.

To avoid being charged, you can destroy the EC2 instance with terraform destroy.
```
terraform destroy
```

