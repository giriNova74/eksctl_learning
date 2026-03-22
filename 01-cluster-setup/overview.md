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

🎯 High-Level Architecture

The EKS cluster setup consists of:

A managed Kubernetes control plane (Amazon EKS)
A dedicated Virtual Private Cloud (VPC)
Worker nodes (EC2 instances) grouped in a managed node group
IAM roles for secure access and permissions
Supporting AWS services like CloudFormation, Auto Scaling, and networking components

---

☸️ 1. Amazon EKS (Control Plane)

Amazon EKS provides a fully managed Kubernetes control plane.

Components managed by AWS:
Kubernetes API Server
etcd (cluster state database)
Scheduler
Controller Manager
Purpose:
Handles all Kubernetes API requests
Maintains cluster state
Schedules workloads onto worker nodes
Key Benefit:
High availability and scalability without managing control plane infrastructure

---

🌐 2. VPC (Virtual Private Cloud)

A dedicated VPC is automatically created by eksctl.

Components created:
Public subnets
Private subnets
Internet Gateway (IGW)
NAT Gateway
Route tables
Purpose:
Provides network isolation for the cluster
Enables secure communication between resources
Allows worker nodes to access the internet (via NAT Gateway)

---

🌍 3. Subnets
Public Subnets:
Used for resources that require internet access
Connected to the Internet Gateway
Private Subnets:
Used for worker nodes (EC2 instances)
Not directly accessible from the internet
Outbound internet access provided via NAT Gateway
Purpose:
Enhances security by isolating compute resources
Supports multi-AZ deployment for high availability

---

🌐 4. Internet Gateway (IGW)
Purpose:
Enables communication between the VPC and the internet
Required for public-facing resources

---

🔁 5. NAT Gateway
Purpose:
Allows private subnet resources (worker nodes) to access the internet
Used for:
Pulling container images
Accessing external APIs

---

🖥️ 6. EC2 Worker Nodes

Worker nodes are EC2 instances where Kubernetes workloads run.

Default Configuration:
Number of nodes: 2
Instance type: t3.medium
Deployed across multiple Availability Zones
Components running on nodes:
kubelet (node agent)
container runtime
kube-proxy (networking)
Purpose:
Execute application workloads (pods)
Communicate with the control plane

---

🔁 7. Managed Node Group

eksctl creates a managed node group backed by an Auto Scaling Group.

Features:
Automatic scaling
Self-healing (replaces failed nodes)
Rolling updates
Purpose:
Simplifies node lifecycle management
Ensures cluster reliability and scalability

---

📊 8. Auto Scaling Group (ASG)
Purpose:
Maintains desired number of EC2 instances
Automatically replaces unhealthy nodes
Supports scaling operations

---

🔐 9. IAM Roles and Permissions

Two main IAM roles are created:

Cluster Role:
Used by the EKS control plane
Allows EKS to manage AWS resources
Node Role:
Attached to EC2 worker nodes
Permissions include:
Pulling container images
Communicating with EKS
Writing logs to AWS services
Purpose:
Secure interaction between AWS services and Kubernetes components

---

📦 10. CloudFormation

eksctl uses AWS CloudFormation to provision all infrastructure.

Purpose:
Automates resource creation
Manages dependencies between resources
Enables easy cleanup and rollback

---

🔒 11. Security Groups
Purpose:
Control inbound and outbound traffic
Define communication rules between:
Control plane and nodes
Nodes and external services

---

📦 12. Kubernetes System Components

After cluster creation, system pods run in the kube-system namespace:

CoreDNS → Handles DNS resolution within the cluster
kube-proxy → Manages networking rules
aws-node → AWS VPC CNI plugin for pod networking
Purpose:
Ensure internal cluster functionality
Enable networking and service discovery

---

🔄 How Everything Works Together
User interacts with the cluster using kubectl
Requests are sent to the EKS control plane (API server)
Scheduler assigns workloads to worker nodes
Pods are deployed on EC2 instances
Networking is handled via VPC and CNI plugin
IAM roles ensure secure communication between services

---

📊 Resources Created in This Setup
1 Amazon EKS Cluster
1 VPC
Multiple public and private subnets
1 Internet Gateway
1 NAT Gateway
1 Managed Node Group
2 EC2 Worker Nodes
IAM Roles (Cluster Role and Node Role)
Security Groups
CloudFormation Stack


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
