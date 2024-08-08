# Three-tier-kubernetes-project
Based on tools like docker, kubernetes, Ec2, EKS, ECR, Cloud Formation,  frontend: React js, backend : Node js, Database: Mongo DB     

Project repo reference : https://github.com/LondheShubham153/TWSThreeTierAppChallenge/blob/main/README.md

# Application code - 

The Application-Code directory contains the source code for the Three-Tier Web Application. Dive into this directory to explore the frontend and backend implementations.

# Kubernetes Manifests Files -

The Kubernetes-Manifests-Files directory holds Kubernetes manifests for deploying your application on AWS EKS. Understand and customize these files to suit your project needs.

# Project Details- 
🛠️ Tools Explored:
- Docker, AWS CLI for AWS infrastructure
- EKS Cluster creation & Load Balancer configuration
- Kubectl, Ingress controller
- Private ECR repositories for secure image management

# Step 1: IAM Configuration

Create a user eks-admin with AdministratorAccess.
Generate Security Credentials: Access Key and Secret Access Key.

# Step 2: EC2 Setup

Launch an Ubuntu instance in your favourite region (eg. region us-west-2).
SSH into the instance from your local machine.


# Step 3: Install AWS CLI v2

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install


# Step 4: Install Docker

sudo apt-get update
sudo apt install docker.io
docker ps
sudo chown $USER /var/run/docker.sock
