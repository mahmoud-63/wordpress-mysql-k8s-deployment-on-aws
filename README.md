# WordPress & MySQL Deployment on Kubernetes (AWS)

This project demonstrates a full deployment of **WordPress** and **MySQL** on **Kubernetes**, using AWS **EBS** and **EFS** for persistent storage.  
The setup includes all essential components — Secrets, Persistent Volumes, PVCs, Deployments, and Services — to run a scalable and persistent WordPress application.

---

##  Project Architecture

Client --> LoadBalancer (wp-svc) --> WordPress Pods --> MySQL Service (ClusterIP) --> MySQL Pod


- **MySQL** uses AWS **EBS** for block storage (RWO).
- **WordPress** uses AWS **EFS** for shared file storage (RWX).
- **Secrets** store MySQL credentials securely.

---

##  Files Overview

| File | Description |
|------|--------------|
| `mysql-deployment.yaml` | MySQL Deployment, Service, PVC, and Secret. |
| `wordpress-deployment.yaml` | WordPress Deployment, PV, PVC, and LoadBalancer Service. |

---

##  Technologies Used

- **Kubernetes** (Deployments, Services, Secrets, PVCs, PVs)
- **AWS EBS CSI Driver**
- **AWS EFS CSI Driver**
- **WordPress** (PHP 7.1 Apache image)
- **MySQL 5.6**
- **YAML configuration**

---

##  Prerequisites

Before you deploy, make sure you have:
- A running Kubernetes cluster (EKS / Minikube / Kind)
- `kubectl` installed and configured
- AWS CSI Drivers installed:
  - [EBS CSI Driver](https://github.com/kubernetes-sigs/aws-ebs-csi-driver)
  - [EFS CSI Driver](https://github.com/kubernetes-sigs/aws-efs-csi-driver)
- Proper IAM permissions for your nodes

---

##  Deployment Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/<your-username>/wordpress-mysql-k8s-deployment-on-aws.git
   cd wordpress-mysql-k8s-deployment-on-aws

    Apply MySQL resources

kubectl apply -f mysql-deployment.yaml

Apply WordPress resources

kubectl apply -f wordpress-deployment.yaml

Verify pods and services

    kubectl get pods
    kubectl get svc

    Access the WordPress site

        Use the LoadBalancer External IP shown in kubectl get svc wp-svc

        Open in your browser: http://<EXTERNAL-IP>

 Expected Output

    wp-deploy running 3 WordPress pods.

    mysql-deploy running 1 MySQL pod.

    Persistent storage on AWS.

    WordPress accessible via public LoadBalancer.

 Security Note

    The MySQL password is stored as a Kubernetes Secret (mysql-secret).

    You can change it by updating the base64-encoded password in the YAML file:

echo -n 'yourpassword' | base64

