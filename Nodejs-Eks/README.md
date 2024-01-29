# Creating and deploying a sample Node.js application on an Amazon EKS cluster using Terraform and Helm charts with High Availability (HA).

Prerequisites:

(1)AWS CLI installed and configured.

(2)Terraform installed.

(3)kubectl installed.

(4)Helm installed.

(5)A sample Node.js application with a Dockerfile.

Steps:

## (1). Set up Node.js application:

Create a Dockerfile for application.

Build and push the Docker image to ECR repository.

### (2)Install Terraform:
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update

Set up Terraform:

Create a directory for Terraform configuration.

Create a main.tf file with EKS cluster configuration.

vim main.tf

provider.tf

subnet.tf

vpc.tf

rout.tf

sg.tf

internetgw.tf

iam.tf

eks_cluster.tf

eks_node_group.tf

# Use Following Commands to Create EKS Cluster Using Terraform:

.terraform init

.terraform validate

.terraform plan 

.terraform apply  (To create the EKS cluster)

#### (3).AWS CLI installed and configured:

curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
unzip awscli-bundle.zip

sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
aws --version

ssh -i Keyname UserName@publicIp

Run aws configure

And then put aws_access_key_id and aws_secret_key_id.

##### (4).Configure kubectl:

curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.29.0/2024-01-04/bin/linux/amd64/kubectl

openssl sha1 -sha256 kubectl

sha256sum -c kubectl.sha256

chmod +x ./kubectl

mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH

# Use this command with your region and cluster name to setup kubectl:-

aws eks --region ap-southeast-1 describe-cluster --name pc-eks --query cluster.status

aws eks --region ap-southeast-1 update-kubeconfig --name pc-eks 

kubectl get nodes

kubectl get svc
