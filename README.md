# JumpBox (Bastion host) in isolated VPC

AWS CloudFormation script that creates a highly available JumpBox server.

The VPC is created using the script in [VPC](https://github.com/gford1000-aws/vpc), creating 3 public subnets.

The script creates a nested stack, constructing the VPC separately from the other resources providing the JumpBox, for clarity.

The script creates the following:

![alt text](https://github.com/gford1000-aws/robust-jumpbox-in-isolated-vpc/blob/master/Screen%20Shot%202017-06-11%20at%206.33.25%20PM.png "Script per designer")

Notes:



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
