# ⚙️ Prerequisites for EKS Cluster Setup

Before creating an EKS cluster using eksctl, ensure the following tools and configurations are in place.

---

## 🧾 1. AWS Account

* An active AWS account is required
* Create an IAM user with:

  * Programmatic access
  * Permissions: AdministratorAccess (for learning purposes)

---

## 🔐 2. Configure AWS Credentials

Run the following command:

aws configure

Provide:

* AWS Access Key
* AWS Secret Access Key
* Default region (e.g., us-east-1 or eu-west-2)
* Output format: json

Verify:

aws sts get-caller-identity

---

## 🛠️ 3. Install AWS CLI

### 🔹 Linux / WSL

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

### 🔹 Verify Installation

aws --version

---

## ☸️ 4. Install kubectl

### 🔹 Linux / WSL

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

chmod +x kubectl
sudo mv kubectl /usr/local/bin/

### 🔹 Verify Installation

kubectl version --client

---

## 🚀 5. Install eksctl

### 🔹 Linux / WSL

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin

### 🔹 Verify Installation

eksctl version

---

## 🌐 6. Network & System Requirements

* Stable internet connection
* Terminal (Linux / WSL / macOS / PowerShell)

---

## 🧠 7. Basic Knowledge (Recommended)

* Kubernetes basics (Pods, Nodes, Services)
* AWS fundamentals (EC2, IAM, VPC)

---

## ✅ Final Checklist

Ensure all commands work:

aws --version
kubectl version --client
eksctl version

---

## 🎯 Outcome

Once all prerequisites are completed, you are ready to create and manage Kubernetes clusters on AWS using eksctl.
