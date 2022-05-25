# mariadb-aws-cloudformation-templates

# xpand-vX.yaml - "X" is version number
## This is a template to create a 3 node xpand cluster with a maxscale node

## Prerequisites
1. Install aws cli tools
2. Set AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN in your environment that issues aws cli commands
3. Can also set AWS_DEFAULT_REGION
4. Create a public/private keypair to associate to your the security groups


## Getting started
Set "Default"  values for all the  "Parameters" at top of template

========================================================

# primary-replica-vX.yaml - "X" is version number
## This is a template to create a 3 node cluster with one primary and two replicas and a maxscale node

## Prerequisites
1. Install aws cli tools
2. Set AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN in your environment that issues aws cli commands
3. Can also set AWS_DEFAULT_REGION
4. Create a public/private keypair to associate to your the security groups

## Getting started
Set "Default"  values for all the  "Parameters" at top of template