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

![image](https://github.com/user-attachments/assets/8ef33172-2f5c-486b-9d69-cf20384a23d7


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
  - to check backend run successfully or not

  ```bash
  docker logs backend_container_id
  ```
  
  docker run 
  ![image](https://github.com/user-attachments/assets/c68f39e0-4dcb-46cb-9a02-d14382ab8417)
  
<h5 style="color:red;">Note:</h5>   We will get a error which could not connect  mongo Db Database 


### Step 10 : Rum Mangodb database using Deployment file

Go to this location on CMD:
root@ip-172-31-37-93:~/TWSThreeTierAppChallenge/Kubernetes-Manifests-file/Database#  

Create Namespace and update in databse Deployment file

 ```bash
kubectl create namespace three-tier-ns
```

![image](https://github.com/user-attachments/assets/d20e11e2-625e-4150-a796-f347a5815545)


![image](https://github.com/user-attachments/assets/cbc6a80c-07d8-4200-bd06-eaefbe8fb003)

- Run deployment file of mongodb-database using follwing command

```bash
kubectl apply -f deployment.yaml -n three-tier-ns

kubectl get pods -n three-tier-ns
```

![image](https://github.com/user-attachments/assets/0a33d0fc-411c-4958-8f3a-6b53fefe6c34)
 <h5 style="color:red;">Note:</h5>   when u run command get pods, then you can see your POD will be in pending state because, we have to apply secrete file.



- Run secrete file using command


```bash
kubectl apply -f secrets.yaml -n three-tier-ns
````

<h5 style="color:red;">Note:</h5>  make sure change namespace in secrete.yml file

![image](https://github.com/user-attachments/assets/786662e1-0b65-402f-9de1-1da821bc710b)

<h5 style="color:red;">Note:</h5> After run secrets.yaml your databse pod will be create in running state 

![image](https://github.com/user-attachments/assets/6c367745-5498-4f6b-bba2-d5591b8ed7bf)


- Run service.yml file of database

<h5 style="color:red;">Note:</h5>  make sure change namespace in secrete.yml file

![image](https://github.com/user-attachments/assets/4fc5063c-50ac-47ee-a80b-5f5105cb8aa0)

```bash
kubectl apply -f service.yaml -n three-tier-ns

kubectl get svc -n three-tier-ns
````

![image](https://github.com/user-attachments/assets/bcd3a7b5-5bf3-472c-bee0-285a0c312b4e)



### Step 11 : Run Backend deployment.yml and service.yml file 

Go to this location on CMD:
root@ip-172-31-37-93:~/TWSThreeTierAppChallenge/Kubernetes-Manifests-file/Backend#

<h5 style="color:red;">Note:  open deplyment.yml file and change your Imange ID in file, copy backend-imaage from ECR

  ![image](https://github.com/user-attachments/assets/2a4a873d-1b0a-4625-9476-0298533f4718)

  ![image](https://github.com/user-attachments/assets/85e1426c-b3e9-4b36-a058-c11e6ea4f6d2)


  ![image](https://github.com/user-attachments/assets/585d43a6-d649-489e-8ce6-eb714dc8dfa9)


<h5 style="color:red;">Note:</h5>  make sure change namespace in secrete.yml file

  ![image](https://github.com/user-attachments/assets/981cfe80-bd04-4b29-be41-9d7e8c2fef64)


- Now run deployment.yml file using following command

```bash
kubectl apply -f deployment.yml -n three-tier-ns

kubectl get deployment -n three-tier-ns
````

![image](https://github.com/user-attachments/assets/90cc43f7-cf20-4596-9a47-504c8858b928)


- Run service.yml file of backend

- <h5 style="color:red;">Note:</h5>  make sure change namespace in secrete.yml file

```bash
kubectl apply -f service.yml -n three-tier-ns

kubectl get svc -n three-tier-ns
````
![image](https://github.com/user-attachments/assets/8a33147e-3c94-4fa9-95a2-02b92dd99a61)


- Check your databse connect to your backend

```bash
kubectl logs api-76b4897595-fx2th -n three-tier-ns
```

![image](https://github.com/user-attachments/assets/31201bad-2acc-4582-993a-bb30fe9ec53a)




### Step 12 : Run Frontend deployment.yml and service.yml file 

Go to this location on CMD:
root@ip-172-31-37-93:~/TWSThreeTierAppChallenge/Kubernetes-Manifests-file/Frontend

<h5 style="color:red;">Note:  open deplyment.yml file and change your Imange ID in file and, copy backend-imaage from ECR and mention domain name with subdomain

![image](https://github.com/user-attachments/assets/a5fbe2df-52c1-42d7-8a75-c65325c93a2c)

  
![image](https://github.com/user-attachments/assets/11c001d8-86d4-472e-814c-3035a2565b55)

- Run Deployment.yaml and service.yaml file of frontend

```bash
kubectl apply -f deployment.yml -n three-tier-ns

kubectl get deployment -n three-tier-ns
````

```bash
kubectl apply -f service.yml -n three-tier-ns

kubectl get svc -n three-tier-ns
````

![image](https://github.com/user-attachments/assets/6fb95572-977b-47e3-aaaf-66ec76d99b21)

<h5 style="color:red;">Note: till now frontend pod is running state , backend and databse is now running properly and connected to each other

![image](https://github.com/user-attachments/assets/e0461422-2681-4db7-bbc6-96da74e1ab75)



# Step 13 :  To Install AWS Load Balancer and Deploy AWS Load Balancer Controller follow below steps

  ### Steps to setup ingress controller


1. create an OIDC provider, use below link and follow steps
https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html

![image](https://github.com/user-attachments/assets/ee5e124d-4163-4b34-a8ed-568b3e651964)

2. Create IAM role

<h5 style="color:red;">Link :  https://docs.aws.amazon.com/eks/latest/userguide/lbc-manifest.html

```bash
curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.7.2/docs/install/iam_policy.json
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy10 \
    --policy-document file://iam_policy.json
```

![image](https://github.com/user-attachments/assets/251e81bf-c07b-4f33-81cf-d966b5ca68e8)


<h5 style="color:red;">Note:   replace the ARN with policy's ARN below

```bash
eksctl create iamserviceaccount \
  --cluster=three-tier-cluster \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --role-name AmazonEKSLoadBalancerControllerRole10 \
  --attach-policy-arn=arn:aws:iam::590184143627:policy/AWSLoadBalancerControllerIAMPolicy10 \
  --approve
```

  ![image](https://github.com/user-attachments/assets/d668f982-1a6d-4c76-a652-df85db34c350)



3. Install cert manager

```bash   
kubectl apply \
    --validate=false \
    -f https://github.com/jetstack/cert-manager/releases/download/v1.13.5/cert-manager.yaml
```

![image](https://github.com/user-attachments/assets/5c216c0e-ef1d-4a8b-9a65-3a3e11c72064)


4. install AWS load balancer controller

```bash
curl -Lo v2_7_2_full.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.7.2/v2_7_2_full.yaml

sed -i.bak -e '612,620d' ./v2_7_2_full.yaml

sed -i.bak -e 's|your-cluster-name|my-cluster|' ./v2_7_2_full.yaml

kubectl apply -f v2_7_2_full.yaml

curl -Lo v2_7_2_ingclass.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.7.2/v2_7_2_ingclass.yaml

kubectl apply -f v2_7_2_ingclass.yaml
```


![image](https://github.com/user-attachments/assets/9cfe3af1-9391-4bc3-802c-bc3c5c7fa777)


5. verify

```bash
kubectl get deployment -n kube-system aws-load-balancer-controller
```

![image](https://github.com/user-attachments/assets/632379c5-720f-4cc2-ae0e-6755967e649d)


![image](https://github.com/user-attachments/assets/1ec39229-9d78-479e-befb-fe676b9d8976)





#Step 14: Run Ingress.yaml file

Go to this location on CMD:
root@ip-172-31-37-93:~/TWSThreeTierAppChallenge/Kubernetes-Manifests-file#

```bash
kubectl apply -f ingress.yaml -n three-tier-ns
kubectl get ing -n three-tier-ns
```

![image](https://github.com/user-attachments/assets/ab2cde71-6e24-42ab-acda-49f8d45ab9a7)


# Step 14: we need to create Hosted zone in Route 53 Aws Service 

- create hosted zone

  ![image](https://github.com/user-attachments/assets/8cfeaf40-6765-4f59-a186-330144b1fb2c)

- exchange ns rocords of your hostinger with Route 53 Hosted zone

  ex. Hosted zone Ns records   ->  Hostinger ns records
  
![image](https://github.com/user-attachments/assets/8bc4c001-f9c0-4d11-a64c-44fe0b766493)

![image](https://github.com/user-attachments/assets/5287bdb6-8ed9-4369-81b9-164be897e3e4)

- Create cname record in hosted zone
   - provide sub-domain name : (challenge)
   - provide your address of load balancer (k8s-threetie-mainlb-318ada61f9-1596259174.ap-south-1.elb.amazonaws.co)

![image](https://github.com/user-attachments/assets/40361210-eadc-493a-a7a0-1da672a1f375)



- Now hit domain name on chrome browser (**challenge.akshaydhongade.online**)

![image](https://github.com/user-attachments/assets/83bb7535-7bbb-4a36-83f2-59b875da1323)

  
- Create some operations on todo list app
  
![image](https://github.com/user-attachments/assets/03f6ee4c-2898-4575-a5fc-24a732863ddb)
  

# Step 15 : check into your database created entry is exist in database table or not

1) Below Command is use to go inside mongo db pod
  
```bash
  kubectl exec -it <pod_name> -n <namespace> -- bash
```

2) After going inside mongo db pod we need to use mongo keyword

```bash
  mongo
```
3) To see all Databases inside mongo Db Env

   ```bash
    show dbs
   ```

4) to use specific database use below command

    ```bash
    use todo
    ```
5) To see tables inside that specific choees database use below command 

   ```bash
   show collections
   ```
6) To see Records of table use below command

    ```bash
   db.tasks.find()
    ```     
![image](https://github.com/user-attachments/assets/7534c508-f28c-4afa-8ec4-cb218d171379)  

7) Go to frontend and try to delete some todo records and check inside mongo db databse tasks table , entry deleted successfully or not

    ![image](https://github.com/user-attachments/assets/360284b2-5a69-4e75-9ed7-dae715b284cd)

    ![image](https://github.com/user-attachments/assets/3e0c68ea-51f3-49d0-94df-9837c7dcecca)

    ![image](https://github.com/user-attachments/assets/526a39a6-20fc-498a-ae1c-b11dd7aad08d)

8) try to add and delete entry and check again

   ![image](https://github.com/user-attachments/assets/3ea227d2-b633-4489-bb9c-987d1c9508ec)

   ![image](https://github.com/user-attachments/assets/468d942e-91c9-4f97-b018-25069fcf729f)

  ![image](https://github.com/user-attachments/assets/07323085-3e77-437b-9531-86fffbb8be91)

<h1> Project Successfully complete </h1>























