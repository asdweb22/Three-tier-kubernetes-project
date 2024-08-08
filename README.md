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

![image](https://github.com/user-attachments/assets/e8a7c916-cdd8-48d8-97eb-4cb878a13d5e)

Generate Security Credentials: Access Key and Secret Access Key.

![image](https://github.com/user-attachments/assets/a736221d-1273-42ba-8d63-b1d5a79d15fc)


# Step 2: EC2 Setup

```bash
Launch an Ubuntu instance in your favourite region (eg. region ap-south-1).
```

![image](https://github.com/user-attachments/assets/bff7b9b5-713b-458c-8304-ef784be064eb)
![image](https://github.com/user-attachments/assets/31ce0327-fd63-42e6-a946-007692b4f560)
![image](https://github.com/user-attachments/assets/a7488d22-4649-4798-98b0-8c544731df5a)
![image](https://github.com/user-attachments/assets/14dd20ad-3f91-40e8-91f4-5e0642b64ac4)


SSH into the instance from your local machine.

![image](https://github.com/user-attachments/assets/45d51d57-31df-4a7d-9994-5db5f52089c1)


# Step 3: Install AWS CLI v2

```bash
sudo -i
apt update
apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

![image](https://github.com/user-attachments/assets/a7c8e320-d5ad-4b90-9a2e-a49ad5297f00)



### Step 4: Install Docker

```bash
sudo apt-get update
sudo apt install docker.io
```

![image](https://github.com/user-attachments/assets/9c43f22d-94d4-4718-a12d-c1782b592741)


### Step 5: Install kubectl

```bash
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client
```

![image](https://github.com/user-attachments/assets/80fe0cf6-a5e3-4e96-9450-8bd8c95f05cc)


### Step 6: Install eksctl

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

![image](https://github.com/user-attachments/assets/b2bfe6a8-1bb5-4d6a-bcb9-1d91db04c3bc)



### Step 7: configure aws

```bash
aws configure
```

![image](https://github.com/user-attachments/assets/e8132954-2fb6-42a6-a869-4ac2769aba76)


### Step 8: Setup EKS Cluster

```bash
eksctl create cluster --name three-tier-cluster --region us-west-2 --node-type t2.medium --nodes-min 2 --nodes-max 2
aws eks update-kubeconfig --region us-west-2 --name three-tier-cluster
kubectl get nodes
```








