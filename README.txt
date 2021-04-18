
AWS CLI installed via pip
AWS SDK installed via pip
Ansible installed via pip
Ansible base config link: https://raw.githubusercontent.com/linuxacademy/content-deploying-to-aws-ansible-terraform/master/aws_la_cloudplayground_version/ansible.cfg
Terraform link: https://releases.hashicorp.com/terraform/0.12.29/terraform_0.12.29_linux_amd64.zip
Ensure the terraform binary is in (/usr/local/bin) path, once uzip'd


#Versions

AWS CLI - v1.19.45
Python-3 (pip) - v21.0.1
Ansible - v2.10.7
Terraform - v0.12.29
Botocore - v1.20.53

#Variables.tf

Listing variables to be used throughout the other Terraform files
region-master is our master node for jenkins deployed in us-east-1 region
region-worker is our slave node for jenkins deployed in us-west-2 region
external_ip is currently utilizing "any" ip, but can set this to your local ip to tighten security


#Networks.tf

This shows the backbone of the network infra (VPCs, IGWs, AZs, Subnets, RTs, and VPC peering)
Will add network flow to this note later


#Backend.tf

Terraform state file stored in S3 bucket 'terraformstatebucker696969'


#Providers.tf

Creates two regions, region-master for jenkins master node in us-east-1 and region-worker for jenkins worker node in us-west-2


#Security_groups.tf

First security group is for load balancer, allowing tcp 80 and 443, with any outbound access in the us-east-1 vpc
Second security group is for jenkins master in us-east-1 allowing 8080 from load balancer, 22 from anywhere (can dial this down to your public IP in variables for 'external_ip'), any ports from us-west-2 private subnet, and any egress
Third security group is for jenkins worker in us-west-2 allowing 22 from your public ip, any traffic from us-east-1 private subnet, and any egress


#Instances.tf

Bootstrapping of jenkins master and worker EC2 instances in the respective regions, runs local provisioner with the respective ansible playbooks in ansbile_templates folder
Includes AMI Ids via SSM and keypair creation for SSH access via terraform controller


#Outputs.tf

Outputs the public IP addresses of jenkins master and worker EC2 instances once deployed


#Ansible.cfg

Enables dynamic inventory calling in the tf_aws_ec2.yml file via aws_ec2 plugin


#Tf_aws_ec2.yml

enables aws_ec2 plugin for dynamic inventory on terraform local provisioner in both regions (us-east-1, us-west-2)
source: https://raw.githubusercontent.com/linuxacademy/content-deploying-to-aws-ansible-terraform/master/aws_la_cloudplayground_multiple_workers_version/ansible_templates/inventory_aws/tf_aws_ec2.yml


#Jenkins-master-sample.yml

playbook that installs git on master EC2 instance (us-east-1) and becomes root user


#Jenkins-worker-sample.yml

playbook that installs jq on worker EC2 instances (us-west-2) and becomes root user


#Network Diagram available in "images" folder
