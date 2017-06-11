# JumpBox (Bastion host) in isolated VPC

AWS CloudFormation script that creates a highly available JumpBox server.

The VPC is created using the script in [VPC](https://github.com/gford1000-aws/vpc), creating 3 public subnets.

The script creates a nested stack, constructing the VPC separately from the other resources providing the JumpBox, for clarity.

The script creates the following:

![alt text](https://github.com/gford1000-aws/robust-jumpbox-in-isolated-vpc/blob/master/Screen%20Shot%202017-06-11%20at%206.33.25%20PM.png "Script per designer")

Notes:

1. Access to the VPC can be restricted to a specific CIDR block range
2. The script creates a Network ACL that only allows access to the VPC using SSH or RDP, and allows no access from the VPC.  Therefore the JumpBox can be reached securely but once on the JumpBox, no egress is permitted, which minimises the potential for data loss or unwanted downloads.
3. The JumpBox is launched via an AutoScalingGroup across the 3 public subnets, which ensures a single JumpBox instance is running.  The Launch Configuration does not create public IP addresses, so cannot be reached directly by a VPC IP.
4. The script creates an Elastic IP, which is associated to the running JumpBox instance.
5. The script creates a Lambda function that listens to Launch events from the Autoscaling Group (via an SNS topic), associating the Elastic IP to the newly started instance.
6. Cloudwatch logs capture the association performed by the Lambda function.


## Arguments

| Argument           | Description                                                        |
| ------------------ |:------------------------------------------------------------------:|
| AllowedCIDRRange   | The CIDR address block that can access the VPC                     |
| CidrAddress        | First 2 elements of CIDR block, which is extended to be X.Y.0.0/16 |
| InstanceAmiId      | The AMI used for the JumpBox instance                              |
| InstanceType       | The instance type (default t2.micro) for the JumpBox instance      |
| KeyName            | The KeyName required to access the JumpBox instance                |               
| VPCTemplateURL     | The S3 URL to the VPC template                                     |


## Outputs

| Output                  | Description                                                 |
| ----------------------- |:-----------------------------------------------------------:|
| EIP                     | The Elastic IP address associated with the JumpBox instance |
| JumpBoxRole             | The IAM role associated wit the JumpBox instance            |
| JumpBoxSecurityGroup    | The Security Group associated with the JumpBox instance     |
| RouteTable              | The Route Table of the VPC                                  |
| VPC                     | The reference to the VPC                                    |
| VPCNacl                 | The Network ACL for the VPC                                 |


## Licence

This project is released under the MIT license. See [LICENSE](LICENSE) for details.
