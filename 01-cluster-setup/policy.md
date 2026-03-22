# 🔐 IAM Policies Required for EKS Cluster Creation

## 📌 Overview

Creating an Amazon EKS cluster using eksctl requires permissions across multiple AWS services.

This is because eksctl uses AWS CloudFormation to provision infrastructure such as:

* VPC
* Subnets
* EC2 instances (worker nodes)
* IAM roles
* Security groups

---

## 🎯 Why Permissions Are Needed

When you run:

eksctl create cluster

It internally:

* Creates IAM roles for EKS
* Launches EC2 instances
* Configures networking (VPC, subnets)
* Uses CloudFormation stacks
* Applies resource tagging

---

## 🧱 Required AWS Services Permissions

The IAM user must have access to:

* Amazon EKS → eks:*
* EC2 → ec2:*
* IAM → iam:* (especially role creation & pass role)
* CloudFormation → cloudformation:*
* Auto Scaling → autoscaling:*
* ELB → elasticloadbalancing:*

---

## ⚠️ Common Errors (If Permissions Missing)

* iam:CreateRole → cluster creation fails
* UnauthorizedTaggingOperation → tagging permission missing
* Resource creation cancelled → dependency failure

---

# 🛠️ METHOD 1: Inline Policy (Custom JSON)

Attach this inline policy to your IAM user:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "eks:*",
        "ec2:*",
        "cloudformation:*",
        "autoscaling:*",
        "elasticloadbalancing:*"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:CreateRole",
        "iam:AttachRolePolicy",
        "iam:PutRolePolicy",
        "iam:TagRole",
        "iam:PassRole",
        "iam:GetRole",
        "iam:ListRoles"
      ],
      "Resource": "*"
    }
  ]
}
```

---

## 📌 When to Use Inline Policy

* Learning environments
* Personal projects
* When you want full control over permissions

---

# 🧰 METHOD 2: Attach AWS Managed Policies (Recommended)

Instead of custom JSON, attach these policies:

### ✅ Required Managed Policies

* AmazonEKSFullAccess
* AmazonEC2FullAccess
* IAMFullAccess
* AWSCloudFormationFullAccess

---

## 📍 Steps to Attach Policies

1. Go to AWS Console

2. Navigate to IAM → Users

3. Select your user

4. Click **Add permissions**

5. Choose **Attach policies directly**

6. Select the following:

   * AmazonEKSFullAccess
   * AmazonEC2FullAccess
   * IAMFullAccess
   * AWSCloudFormationFullAccess

7. Click **Add permissions**

---

# ⚖️ Inline vs Managed Policies

| Approach       | Pros              | Cons              |
| -------------- | ----------------- | ----------------- |
| Inline Policy  | Full control      | Harder to manage  |
| Managed Policy | Easy, quick setup | Broad permissions |

---

# 🔥 Best Practice (Real-World DevOps)

In production environments:

* Avoid wildcard (*) permissions
* Use least privilege principle
* Create fine-grained IAM roles
* Use IAM roles instead of users

---

# ⚠️ Important Note

The policies above are **over-permissive** and intended for:

* Learning
* Lab environments

Do NOT use these directly in production.

---

# 🚀 Summary

To successfully create an EKS cluster using eksctl:

* You need permissions for EKS, EC2, IAM, and CloudFormation
* You can either:

  * Use an inline policy (custom JSON)
  * Attach AWS managed policies (recommended for beginners)

---

## 🎯 Outcome

With correct IAM permissions, eksctl can:

* Create cluster successfully
* Provision infrastructure
* Avoid permission-related failures
