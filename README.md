# mariadb-aws-cloudformation-templates

# xpand-cluster.yaml

This template launches 4 VMs to create a 3 node xpand cluster with on maxscale node. 

It assumes you are deploying to an existing VPC and subnet, which are specified in the "Parameters" section.

You must also choose IP address for each of the nodes that do not conflict with existing nodes on the subnet.

## Prerequisites
1. Install aws cli tools
2. Set AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN in your environment that issues aws cli commands. On MacOs these can be set in your .bash_profile file. In Windows, they are likely set as Environment variables, but not confirmed in this project yet.
3. Can also set AWS_DEFAULT_REGION
4. Create a public/private keypair to associate to your the security groups. Goes in ~/.ssh directory on MacOs

## Launch stack

From a terminal a stack can be created with the following command

```bash
$ cd *directory_where_template_resides*\
$ aws cloudformation create-stack --stack-name *your-stack-name*  --template-body file://xpand-cluster.yaml
```

## Getting started
Set "Default"  values for all the  "Parameters" near top of template.

---

# primary-replica-cluster.yaml

This is a template launches 4 VMs to create a 3 node cluster with one primary and two replicas and a maxscale node.

It assumes you are deploying to an existing VPC and subnet, which are specified in the "Parameters" section.

You must also choose IP address for each of the nodes that do not conflict with existing nodes on the subnet

## Prerequisites
1. Install aws cli tools
2. Set AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN in your environment that issues aws cli commands. On MacOs these can be set in your .bash_profile file. In Windows, they are likely set as Environment variables but not confirmed in this project yet.
3. Can also set AWS_DEFAULT_REGION
4. Create a public/private keypair to associate to your the security groups. Goes in ~/.ssh directory on MacOs

## Getting started
Set "Default"  values for all the  "Parameters" near top of template

## Launch stack

From a terminal a stack can be created with the following command
```bash
$ cd *directory_where_template_resides*
$ aws cloudformation create-stack --stack-name *your-stack-name*  --template-body file://primary-replicat-cluster.yaml
```