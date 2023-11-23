# k8repo

# Setup Minikube on AWS Ec2
## Setup Docker 
- yum update -y
- yum install docker
- sudo docker info
- service docker start
- systemctl start docker
- status docker.service
- newgrp docker
- usermod -a -G docker ec2-user
- docker version

## Install kubectl 
-  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
-  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
-   kubectl version

## Install Minikube
-  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
-  sudo install minikube-linux-amd64 /usr/local/bin/minikube
-  yum install  conntrack
-  minikube start --driver=docker
-  minikube status
-  Verify :  kubectl get pods 
