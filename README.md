In this article, we will show how to create an EC2 instance on Amazon Web Services using Terraform.

*Prerequisites
To create an EC2 instance on AWS with Terraform, we will need following prerequisites in place:

**AWS Account: 
You must have an AWS account to create and manage resources on the AWS cloud. If you don’t already have this, you can sign up for an account and use the free tier here. For the first 12 months, you can run a free EC2 instance of the following specifications:
750 hours per month of Linux, RHEL, or SLES t2.micro or t3.micro instance dependent on region
750 hours per month of Windows t2.micro or t3.micro instance dependent on region
If you continue to run your EC2 instance after the 12-month free tier allowance period is up you’ll start getting charged, so remember to clean up after the tutorial!

**Terraform installed: 
You’ll need to have Terraform installed on your machine to write and execute Terraform code. You can download the appropriate version for your machine here. Extract the downloaded zip file to a directory on your machine and add the directory containing the Terraform binary to your system’s PATH environment variable.
AWS CLI installed & IAM User with permissions: You’ll need to have the AWS Command Line Interface (CLI) installed on your machine to interact with EC2 instances and other AWS resources from the command line. You can download the appropriate version for your system here. Once you have installed the AWS CLI, you can configure it by running the following command in a terminal window:
aws configure
This will prompt you to enter your AWS access key ID, secret access key, default region, and default output format. You can obtain your access key ID and secret access key from the AWS Management Console by navigating to the security credential section once logged in or create a new one from there if needed.

If you have not already done so, you should create an IAM user with the minimum required permissions necessary.

Learn more about AWS IAM best practices.

SSH key pair: To access a Linux-based EC2 instance via SSH, you’ll need an SSH key pair.
Run the following command to generate a new SSH key pair:

ssh-keygen -t rsa -b 4096
This will create a new RSA key pair with a length of 4096 bits.

You will be prompted to enter a file name to save the key pair. The default location is in your user’s home directory under the .ssh directory. You can choose a different file name or directory if you prefer.

You will be prompted to enter a passphrase for the key pair. This is optional but recommended to add an extra layer of security.

The ssh-keygen command will generate two files: a private key file and a public key file. The private key file should be kept secure and never shared with anyone. The public key file can be shared with Amazon EC2 instances to allow SSH access.

Finally, to use the key pair with an Amazon EC2 instance, you must add the public key to the instance when you configure it with Terraform.

Authentication with AWS
You can configure Terraform to authenticate with AWS using several methods. With AWS CLI installed, we can use the named profiles method, which is a recommended approach for authenticating Terraform to AWS because it allows you to manage multiple sets of AWS credentials and control access to resources using IAM roles and policies.

First, ensure the AWS CLI is installed and configured using the guidelines in the prerequisite section to add the AWS access key ID and secret access key using the aws configure command. By default, the AWS CLI-named profiles use the same access key ID and secret access key as your default profile, so you don’t need to specify them again for different profiles.

Create an AWS CLI named profile for Terraform in the ~/.aws/config file (Linux and macOS) or %UserProfile%\.aws\config file (Windows). You can override the default access key ID and secret access key for a named profile by setting the aws_access_key_id and aws_secret_access_key attributes if required.

Although it is not necessary (and may cause problems if one of your team uses the code in a different SDK), you can add a new profile section with a unique profile name, such as jack.roper. The example below tells the AWS CLI to use the us-west-2 region for the jack.roper profile.