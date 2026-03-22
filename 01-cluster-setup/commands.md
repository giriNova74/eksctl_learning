# ⚙️ Commands Used in EKS Cluster Setup

## 🔐 Configure AWS

aws configure

aws sts get-caller-identity

---

## 🚀 Create EKS Cluster

eksctl create cluster 
--name devops-cluster 
--region us-east-1

---

## 📊 Verify Cluster

kubectl get nodes

kubectl get pods -A

kubectl get svc

---

## 🧹 Delete Cluster (Cost Saving)

eksctl delete cluster 
--name devops-cluster 
--region us-east-1

---

