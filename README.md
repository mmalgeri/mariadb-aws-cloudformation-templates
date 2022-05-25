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
5. Search for --token, and input YOUR_TOKEN between the double quotes. Also put correct version if not "10.6"

            ./mariadb_es_repo_setup --token="YOUR_TOKEN" --apply --mariadb-server-version="10.6"
6. Search for "SET GLOBAL LICENSE" and input your license in the format show here. Note: double quotes must be preceeded with a backslash. You likely won't receive your license with these backslashes before the double quotes, so they will have to be entered manually.

            echo "SET GLOBAL LICENSE = '{\"expiration\":\"2022-07-01 16:56:47\",\"company\":\"MariaDB Internal -- do not distribute\",\"email\":\"joe.smith@mariadb.com\",\"person\":\"Joe Smith\",\"signature\":\"302c021416184672938244358663014402144552c9f8a7f6e914d682fd48d82928383020\"}';" >> /setGlobalLicense.sql


## Launch stack

From a terminal a stack can be created with the following command
```bash
$ cd directory_where_template_resides
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
5. Search for --token, and input YOUR_TOKEN between the double quotes. Also put correct version if not "10.6"

            ./mariadb_es_repo_setup --token="YOUR_TOKEN" --apply --mariadb-server-version="10.6"


## Getting started
Set "Default"  values for all the  "Parameters" near top of template

## Launch stack

From a terminal a stack can be created with the following command
```bash
$ cd directory_where_template_resides
$ aws cloudformation create-stack --stack-name your-stack-name  --template-body file://primary-replicat-cluster.yaml
```