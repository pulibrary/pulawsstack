# pulawsstack
A set of Terraform modules for configuring infrastructure with AWS

The PUL AWS Stack is a set of [Terraform](https://terraform.io) modules for configuring infrastructure with AWS.
It's a more 'curated' set of defaults for configuring your AWS environment, while still allowing you to fully customize it.

The PUL AWS Stack comes (will come) with:

## Status of this Repo

- [ ] an auto-scaling group of instances to run your services
- [ ] a multi-az VPC with different subnets for availability
- [ ] an ELB and ECS definition for each service
- [ ] logs that populate in CloudWatch
- [ ] a bastion node for manual SSH access
- [ ] automatic ELB logging to S3

Start from scratch or selectively add it to your existing infrastructure, the Stack is yours to customize and tweak.

## Quickstart

_To run the stack, you'll need AWS access and Terraform installed, check out the [requirements](#requirements) section._

The easiest way to get the Stack up and running is by creating a Terraform definition for it, copy this snippet in a file
named `terraform.tf`:

```hcl
module "stack" {
  source      = "github.com/pulibrary/pulawsstack"
  environment = "prod"
  key_name    = "my-key-name"
  name        = "my-app"
}
```
This is the _base_ configuration, that will provision everything you need to run your services.

From there, you'll want to plan, which will stage the changeset

	% terraform plan

And if the changes look good, apply them to your infrastructure

    % terraform apply

This will automatically setup your basic networking configuration with an auto-scaling default cluster

With this setup, you can now run services from [Princeton
Ansible](https://github.com/pulibrary/princeton_ansible)

## Requirements

Before we start, you'll first need:

- [ ] an [AWS account](http://aws.amazon.com/) with API access
- [ ] locally configured [AWS credentials](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-quick-configuration) or a tool like [aws-vault](https://github.com/99designs/aws-vault)
- [ ] to [create a
  keypair](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair) in AWS
- [ ] download and install [terraform](https://terraform.io/)
