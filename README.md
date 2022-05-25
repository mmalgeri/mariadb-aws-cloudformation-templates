# mariadb-aws-cloudformation-templates

### Two templates are presented

The first is **xpand-cluster.yaml**, which launches a 3 node xpand cluster plus a maxscale node\
The second is **primary-replica-cluster.yaml**, which launches 1 primary, 2 replicas and 1 maxscale node

These template require some manual changes to tokens, license, etc.\
**TBD** - Improvements can be made by storing these values outside of the template and using something like AWS code pipeline

# xpand-cluster.yaml

This template launches 4 VMs to create a 3 node xpand cluster with on maxscale node. 

It assumes you are deploying to an existing VPC and subnet, which are specified in the "Parameters" section.

You must also choose IP address for each of the nodes that do not conflict with existing nodes on the subnet.

## Prerequisites
1. Install aws cli tools
2. Set AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN in your environment that issues aws cli commands. On MacOs these can be set in your .bash_profile file. In Windows, they are likely set as Environment variables, but not confirmed in this project yet.
3. Can also set AWS_DEFAULT_REGION
4. Create a public/private keypair to associate to your the security groups. Goes in ~/.ssh directory on MacOs
5. Search for YOUR_TOKEN, and input YOUR_TOKEN. Also put correct version if not "10.6"

      e.g       ./mariadb_es_repo_setup --token="YOUR_TOKEN" --apply --mariadb-server-version="10.6"

      YOUR_TOKEN is also found in wget URLs

6. Search for "SET GLOBAL LICENSE" and input your license in the format show here. Note: double quotes must be preceeded with a backslash. You likely won't receive your license with these backslashes before the double quotes, so they will have to be entered manually. (NOTE: the license signature listed next won't work)

            echo "SET GLOBAL LICENSE = '{\"expiration\":\"2022-07-01 16:56:47\",\"company\":\"MariaDB Internal -- do not distribute\",\"email\":\"joe.smith@mariadb.com\",\"person\":\"Joe Smith\",\"signature\":\"302c021416184672938244358663014402144552c9f8a7f6e914d682fd48d82928383020\"}';" >> /setGlobalLicense.sql

## Getting started
Set "Default"  values for all the  "Parameters" near top of template.

## Launch stack

From a terminal a stack can be created with the following command
```bash
$ cd directory_where_template_resides
$ aws cloudformation create-stack --stack-name *your-stack-name*  --template-body file://xpand-cluster.yaml
```
GIVE THE COMMAND ABOUT 15 MINUTES TO LAUNCH, DOWNLOAD SOFTWARE, AND CONFIGURE VMS

To verify that the XpandGUI was successfully installed open a browser window and enter the IP address of any node in the cluster.

Replace the IP address shown below with the public IP address of any one of the nodes in the cluster

http://34.207.60.148:8080 credentials are noreply@mariadb.com/mariadb

To verify that the cluster is set up properly ssh into any node and type the following:

```bash
$ sudo su - xpand
$ clx status
```
You should see something like the following output, with the "Status" field showing "OK" for each of the 3 xpand nodes

Cluster Name: cl54f4c902fe1d5e9c\
Cluster Version: 5.3.13\
Cluster Status: OK\
Cluster Size: 3 nodes - 8 CPUs per Node\
Current Node: ip-10-0-2-194 - nid 1\
nid | Hostname | Status | IP Address | TPS | Used | Total\
----+----------------+--------+-------------+-----+----------------+--------\
1 | ip-10-0-2-194 | OK | 10.0.2.194 | 0 | 21.0M (0.00%) | 994.9G\
2 | ip-10-0-2-214 | OK | 10.0.2.214 | 0 | 14.6M (0.00%) | 994.9G\
3 | ip-10-0-2-26  | OK | 10.0.2.26 | 0 | 14.4M (0.00%) | 994.9G\
----+----------------+--------+-------------+-----+----------------+--------\



---

# primary-replica-cluster.yaml

This is a template launches 4 VMs to create a 3 node cluster with one primary and two replicas and a maxscale node.

The UserData bash script for each node follows the install procedure found in the mariadb documentation at\
(https://mariadb.com/docs/deploy/topologies/primary-replica/enterprise-server-10-6/)

It assumes you are deploying to an existing VPC and subnet, which are specified in the "Parameters" section.

You must also choose IP address for each of the nodes that do not conflict with existing nodes on the subnet

## Prerequisites
1. Install aws cli tools
2. Set AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN in your environment that issues aws cli commands. On MacOs these can be set in your .bash_profile file. In Windows, they are likely set as Environment variables but not confirmed in this project yet.
3. Can also set AWS_DEFAULT_REGION
4. Create a public/private keypair to associate to your the security groups. Goes in ~/.ssh directory on MacOs
5. Search for YOUR_TOKEN, and input YOUR_TOKEN. Also put correct version if not "10.6"

      e.g       ./mariadb_es_repo_setup --token="YOUR_TOKEN" --apply --mariadb-server-version="10.6"

      YOUR_TOKEN is also found in wget URLs


## Getting started
Set "Default"  values for all the  "Parameters" near top of template

## Launch stack

From a terminal a stack can be created with the following command
```bash
$ cd directory_where_template_resides
$ aws cloudformation create-stack --stack-name your-stack-name  --template-body file://primary-replica-cluster.yaml
```

GIVE THE COMMAND ABOUT 15 MINUTES TO LAUNCH, DOWNLOAD SOFTWARE, AND CONFIGURE VMS

To verify that the cluster is set up properly ssh into the maxscale node and type the following:

```bash
$ mxctrl status
```