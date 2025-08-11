# Kubernetes Cluster with Minikube on AWS EC2


# 📌 Overview
This project demonstrates how to deploy and manage applications on a Kubernetes cluster using Minikube inside an AWS EC2 instance.
It follows the objectives of TASK 5:

1. Install and configure Minikube on a remote Linux machine.

2. Deploy an application using Kubernetes manifests.

3. Expose it via a Kubernetes service.

4. Verify, scale, and inspect workloads.



# 🛠 Tools & Technologies
AWS EC2 (Ubuntu 22.04 LTS)

Minikube (Docker driver)

kubectl

Docker

Nginx (demo application)



# ⚙️ Prerequisites

AWS EC2 instance (recommended: 4 vCPU / 8 GB RAM / 20 GB disk)

Security group rules:

SSH (TCP 22) from your IP

NodePort (TCP 30007) from your IP

SSH access to the instance

```sudo```   privileges on the server



# 🚀 Step 1 — Install Dependencies

Update and install helper packages

```sudo apt update && sudo apt upgrade -y```
```sudo apt install -y apt-transport-https ca-certificates curl gnupg lsb-release software-properties-common```

Install Docker

# Add Docker GPG key
```sudo mkdir -p /etc/apt/keyrings```
```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg```

# Add Docker repository
```echo \```
 ``` "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu ```
```$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null```

# Install Docker Engine
```sudo apt update```
```sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin```

# Allow current user to run Docker
```sudo usermod -aG docker $USER```
```newgrp docker```



Install kubectl

```curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"```
```sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl```
```kubectl version --client```


Install Minikube

```curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64```
```sudo install minikube-linux-amd64 /usr/local/bin/minikube```
```minikube version```


Install additional helpers

```sudo apt install -y conntrack socat ebtables```


# 🚀 Step 2 — Start Minikube

```minikube start --driver=docker --cpus=4 --memory=8192 --disk-size=20g```
```minikube status```
```kubectl get nodes```


# 📄 Step 3 — Create Kubernetes Manifests


deployment.yaml
service.yaml



# 🚀 Step 4 — Deploy Application

```kubectl apply -f deployment.yaml```
```kubectl apply -f service.yaml```


# 🔍 Step 5 — Verify Deployment


```kubectl get pods -o wide```
```kubectl get deployments```
```kubectl get svc```


inspect the pod

```kubectl describe pod $(kubectl get pods -o name | head -n1)```
```kubectl logs $(kubectl get pods -o name | head -n1)```


# 🌐 Step 6 — Access Application

Get EC2 public IP:

```curl -s http://169.254.169.254/latest/meta-data/public-ipv4```


Visit in your browser:

```http://<EC2_PUBLIC_IP>:30007```


# 📈 Step 7 — Scale Deployment

```kubectl scale deployment nginx-deployment --replicas=4```
```kubectl get pods -o wide```


# 🧹 Step 8 — Cleanup

```minikube stop```
```minikube delete```




# 📦 Deliverables

YAML files: deployment.yaml, service.yaml

Screenshots / command outputs:

kubectl get pods before & after scaling

kubectl get svc

Browser screenshot showing Nginx welcome page

kubectl describe pod output

kubectl logs output





# 📚 References

Minikube Official Docs

Kubernetes Docs

Docker Install Guide


# Screenshots:


<img width="1352" height="560" alt="Screenshot 2025-08-11 164820" src="https://github.com/user-attachments/assets/f477e072-3e18-483b-b0a4-5fd164455658" />



<img width="1285" height="688" alt="Screenshot 2025-08-11 154004" src="https://github.com/user-attachments/assets/bcb7522b-9c84-46fa-ae9f-2121784cd9d2" />



<img width="1359" height="685" alt="Screenshot 2025-08-11 153857" src="https://github.com/user-attachments/assets/fd795cc6-498d-4e8c-8f57-41cd728d57c7" />



<img width="1351" height="346" alt="Screenshot 2025-08-11 153724" src="https://github.com/user-attachments/assets/bb0ce0a6-b77c-434f-8f10-b5f6bacff770" />












