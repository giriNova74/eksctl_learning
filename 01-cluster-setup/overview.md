# 🚀 Task 01: EKS Cluster Setup using eksctl

## 📌 Overview

In this task, we create a fully functional Kubernetes cluster on AWS using eksctl. This is the foundational step for working with Kubernetes in a cloud environment.

eksctl simplifies the process of provisioning an Amazon EKS cluster by automating infrastructure setup such as VPC, IAM roles, and worker nodes.

---

## 🎯 Objective

* Provision an EKS cluster using eksctl
* Configure kubectl to interact with the cluster
* Verify cluster and node readiness

---

## 🧱 Architecture

* AWS EKS (Managed Kubernetes Control Plane)
* EC2 Instances (Worker Nodes)
* VPC, Subnets, IAM Roles (Auto-created by eksctl)

---

## ⚙️ Steps Performed

1. Installed required tools (AWS CLI, kubectl, eksctl)
2. Configured AWS credentials
3. Created EKS cluster using eksctl
4. Verified cluster using kubectl

---

## ✅ Verification Commands

```bash
kubectl get nodes
kubectl get pods -A
```

---

## 📊 Expected Output

* Nodes should be in **Ready** state
* System pods should be running in **kube-system** namespace

---

## ⚠️ Cost Note

EKS clusters incur charges. Always delete the cluster after use:

```bash
eksctl delete cluster --name devops-cluster --region us-east-1
```

---

## 🚀 Outcome

Successfully created and verified a Kubernetes cluster on AWS using eksctl.
