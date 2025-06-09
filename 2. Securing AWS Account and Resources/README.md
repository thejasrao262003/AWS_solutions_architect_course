# 🛡️ AWS Security Essentials – Module Summary

This README summarizes key concepts from your learning across four videos on securing AWS accounts and resources using IAM, policies, permission boundaries, and AWS Organizations.

---

## 📹 Video 1: Securing AWS Accounts and Resources

### 🔑 IAM Concepts

- **Root Account**: Owner of the AWS account, with full permissions. Should be used sparingly and secured with MFA.
- **IAM Users**: Individual AWS identities under the root account with unique credentials (username/password or access keys).
- **IAM Groups**: Collections of IAM users with shared permissions. Policies are attached to groups for efficient access control.
- **IAM Roles**: Temporary identities that can be assumed by users, services, or accounts. Roles grant temporary credentials for specific permissions.

✅ **Example**:  
Assign a developer a "TestingRole" to temporarily access only testing resources instead of giving full permissions.

---

## 📹 Video 2: IAM Policies

### 🧾 Identity-Based Policies
- Attached to users, groups, or roles.
- Define **what actions** an identity can perform and on **which resources**.

### 🧾 Resource-Based Policies
- Attached directly to a resource (like an S3 bucket or Lambda function).
- Define **who** can access the resource and **what actions** they can perform.

```json
// Identity-based policy sample
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["ec2:DescribeInstances"],
      "Resource": "*"
    }
  ]
}
```

```json
// Resource-based policy sample
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ExamplePolicy",
      "Effect": "Allow",
      "Principal": "*",
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

📌 **Policy Evaluation Order**:
1. Explicit Deny
2. Explicit Allow
3. Implicit Deny (default)

---

## 📹 Video 3: IAM Permission Boundaries

- A **permissions boundary** is a managed policy that sets the **maximum permissions** an IAM user or role can have.
- It **does not grant** permissions — it only **limits** them.

✅ **Example**:
- IAM Policy allows `s3:*`
- Permission Boundary allows only `s3:GetObject`
- ➡️ Result: User can **only** perform `s3:GetObject`

---

## 📹 Video 4: AWS Organizations and SCP

### 🏢 AWS Organizations

- Centralized management of **multiple AWS accounts**
- **Consolidated billing** for all accounts
- Supports **Organizational Units (OUs)** for grouping accounts

Structure:
```
Management Account (Root)
  └── Organizational Units (OUs)
         └── Sub-OUs or AWS Accounts
```

---

### 🔐 Service Control Policies (SCPs)

- SCPs are policies that set **maximum permission limits** across all accounts under an AWS Organization.
- They act as **filters**, not permission granters.
- Applied to the **root**, **OUs**, or **individual accounts**

✅ **Example**:
SCP denies launching EC2 instances larger than `t2.micro` → no account under that OU can bypass it, even if IAM allows it.

---

## ✅ Summary

| Feature | IAM Policy | Permission Boundary | SCP |
|--------|------------|----------------------|-----|
| Grants permissions | ✅ Yes | ❌ No | ❌ No |
| Restricts permissions | ❌ No | ✅ Yes | ✅ Yes |
| Applies to | IAM Users/Roles | IAM Users/Roles | Org Units / Accounts |
| Scope | Identity-level | IAM identity only | Organization-wide |

---

📎 Refer to `AWS_policy_evaluation.png` for the policy evaluation order.

---

Made with 💻 based on your learning journey.