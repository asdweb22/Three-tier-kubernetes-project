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

# Architecture of Kubernets Project

![image](https://github.com/user-attachments/assets/8ef33172-2f5c-486b-9d69-cf20384a23d7)


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
eksctl create cluster --name three-tier-cluster --region ap-south-1 --node-type t2.medium --nodes-min 2 --nodes-max 2
aws eks update-kubeconfig --region ap-south-1 --name three-tier-cluster
kubectl get nodes
```

![image](https://github.com/user-attachments/assets/ec627053-d39b-4879-a439-b0e44d6804f3)
![image](https://github.com/user-attachments/assets/af4d9ac5-7d21-426a-bcc3-7674b357e533)


# Now take git clone whole project from given link

![image](https://github.com/user-attachments/assets/662d85a2-7f46-4657-b8e9-b07a0b866b66)


```bash
git clone https://github.com/LondheShubham153/TWSThreeTierAppChallenge.git
```

![image](https://github.com/user-attachments/assets/1102afa5-7933-4536-bc40-233581e6d6f0)

![image](https://github.com/user-attachments/assets/f2597023-6e97-4ef0-a3c3-17cc7dcc6e17)



### Step 9: Create repositories on AWS ECR and push Image on ECR

![image](https://github.com/user-attachments/assets/d28473e3-a5ae-4f71-9d2a-88ed28e05a95)

![image](https://github.com/user-attachments/assets/64a8cf70-6b0e-4fec-a115-705cb1b5fb5d)

run Bellow command step by step after creating reposotory on ECR

![image](https://github.com/user-attachments/assets/388859ca-fd34-47f5-a919-3c2eecbbbfc9)

create container using already created fronend image


```bash
  docker run -d -p 3000:3000 three-tier-frontend:latest 
```

![image](https://github.com/user-attachments/assets/0613b3f4-babf-4e14-b259-f134a01f65c6)


Setup 3000 port in inbound rule of main instance 

![image](https://github.com/user-attachments/assets/92361b10-c484-4d9d-896b-82b3824ceb21)

copy public instance ip : 3000  on crome or any browser
you will see frontend app

![image](https://github.com/user-attachments/assets/c5435eee-fdff-44ea-a5ed-e7f999e03402)


- Create repository on ECR for backend and push Docker image of BACKEND IMAGE


  ![image](https://github.com/user-attachments/assets/3d0eddc6-9933-4e20-99ea-65080428b89c)


  ![image](https://github.com/user-attachments/assets/67d7feaa-3ed1-42a3-9fff-1bb81aac10ba)


  Provide 3500 port in instance security group inbound rule
  
  ![image](https://github.com/user-attachments/assets/8bb29266-5548-4d7c-9a66-630a9268da9a)

  Run Docker container using docker image

  ```bash
  docker run -d -p 3500:3500 three-tier-backend:latest
  ```
  - to check backemnd run successfully or not

  ```bash
  docker logs backend_container_id
  ```
  
  docker run 
  ![image](https://github.com/user-attachments/assets/c68f39e0-4dcb-46cb-9a02-d14382ab8417)
  Note: We will get a error which could not connect  mongo Db Database 




















