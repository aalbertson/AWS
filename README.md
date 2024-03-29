## AWS
AWS related scripts.

**Prerequisites:**
* You need AWS PowerShell Tools installed and the module loaded
* You need an IAM user registered with the proper credentials for EC2 and Route53

### aws_create_instance.ps1
This script will create an EC2 instance, a key pair to connect, add a Route 53 A record for it.

Options:
* -AMI The Amazon image to use, for example CentOS for us-west-2 is available as ami-d2c924b2
* -Subnet The AWS subnet ID to use
* -Type The instance type, for example t2.nano
* -KeyName The connection key pair to use. The key must be saved in the current folder as $KeyName.pem if it exists, or will be created if not
* -Script File name for commands to run on startup
* -Hostname The hostname to add for this host
* -ZoneId The Route53 zone ID on which to add the hostname
* -SecurityGroup The security group ID to use for the new instance

Example:

    .\aws_create_instance.ps1 -AMI ami-d2c924b2 -Subnet subnet-8e3bf3a2 -Type t2.nano -KeyName aws-test -Script c:\scripts\centos_init.sh -Hostname test.example.com -ZoneId Z1W5966G181726

### aws_destroy_instance.ps1
This script will terminate an EC2 instance, delete the attached volumes, remove the A record.

Options:
* -InstanceId The EC2 instance id to terminate
* -Hostname The hostname to remove for this host
* -ZoneId The Route53 zone ID on which to remove the hostname

Example:

    .\aws_destroy_instance.ps1 -InstanceId i-XXXXXX -Hostname test.example.com -ZoneId Z1W5966G181726
