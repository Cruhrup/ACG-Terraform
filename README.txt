
AWS CLI installed via pip
Ansible installed via pip
Ansible base config link: https://raw.githubusercontent.com/linuxacademy/content-deploying-to-aws-ansible-terraform/master/aws_la_cloudplayground_version/ansible.cfg
Terraform link: https://releases.hashicorp.com/terraform/0.12.29/terraform_0.12.29_linux_amd64.zip
Ensure the terraform binary is in (/usr/local/bin) path, once uzip'd


#Versions

AWS CLI - v1.19.45
Python-3 (pip) - v21.0.1
Ansible - v2.10.7
Terraform - v0.12.29

#Variables.tf

Listing variables to be used throughout the other Terraform files
region-master is our master node for jenkins deployed in us-east-1 region
region-worker is our slave node for jenkins deployed in us-west-2 region
external_ip is currently utilizing "any" ip, but can set this to your local ip to tighten security

#Networks.tf

This shows the backbone of the network infra (VPCs, IGWs, AZs, Subnets, RTs, and VPC peering)
Will add network flow to this note later

#Backend.tf


#Providers.tf


#Security_groups.tf















#Network Diagram available in "images" folder
