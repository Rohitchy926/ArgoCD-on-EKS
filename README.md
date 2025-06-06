# ArgoCD-on-EKS
# Installation Instructions

## Step 1: Create EC2 Instance
    
## Step 2: Install ```AWS CLI```, ```Kubectl```, ```EKSCTL```:
- ```AWS CLI``` - AWS CLI is a unified tool for managing AWS services from the command line.

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

apt install unzip

unzip awscliv2.zip
```

- ```Kubectl``` - kubectl is the command-line tool used to interact with Kubernetes clusters.
```
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.30.2/2024-07-12/bin/linux/amd64/kubectl

chmod +x kubectl

mv kubectl /usr/local/bin/kubectl
```    
- ```EKSCTL``` - eksctl is a command-line tool for managing Amazon EKS (Elastic Kubernetes Service) clusters.
```
curl -LO "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz"

tar -xzf eksctl_Linux_amd64.tar.gz

sudo mv eksctl /usr/local/bin/

eksctl version
```
## Step 3: AWS Configure - 
        ○ Access Key - Your_Access_Key
        ○ Access Secret Key - Your Access_secret_key
        
## Step 4: Create EKS Cluster -
- Create Cluster:
```
eksctl create cluster --name test-server --us-east-1 --node-type t2.medium --nodes-min 1 --nodes-max 2
```

- Get Eks Cluster:
```
eksctl get cluster --name test-server --region us-east-1
```
- Update Kubeconfig file for  kubectl:
```
aws eks update-kubeconfig --name test-server --region us-east-1
```
## Step 5: Install ArgoCD
```
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

<img width="1512" alt="image" src="https://github.com/user-attachments/assets/db9cb295-a999-4bc1-bb51-9559ac594e0e" />



- Retrieve the initial admin password for ArgoCD:
```
kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```   
## Step 6: Deploy an App on ArgoCD
Deploy your first application using ```deployment.yaml```.

## Step 7: Once after deploying ArgoCD 
open with - Username - admin
             pass- that you have created with (kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)

<img width="452" alt="image" src="https://github.com/user-attachments/assets/ac9b354d-561e-4145-a72a-95ccec6bbe35" />


## step 8: Created an ArgoCD Application resource that points to a Git repository with the NGINX manifests.

<img width="1512" alt="image" src="https://github.com/user-attachments/assets/257a70b8-e287-41f8-9fd6-faba41fac7e1" />

