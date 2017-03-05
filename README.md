# mock-aws-env
Infrastructure as code - Builds an entire mock AWS environment with templates

## Mock Templates

The AWS Mock architecture is managed using CloudFormation templates.

The diagram below outlines the process to build the entire Mock architecture from the ground up.

[ image ]

1. User starts the build by launching the **wrapper** stack via the AWS console or an API call.
2. The wrapper template launches the **vpc** stack and builds the VPC infrastructure.
3. Once the VPC build has completed, wrapper calls the **security** template to deploy the security groups.
4. After the security stack is completed, all the dependencies required to build rest of the services are in place.  The **elb, cache, rds and bastion** templates are launched.
5. After successful completion, 6 CloudFormation stacks (including the wrapper stack) are created.

## The Topology

[ image ]

Each VPC contains the following resources.

* Two availability zones to provide local redundancy
* Two NAT servers for outbound initiated traffic
* Two servers in an Autoscale group attached to a Load Balancer (ELB)
* Two ElastiCache nodes
* One read-replica Db node (The master should be located in another region.)
* One bastion host for remote access and management

