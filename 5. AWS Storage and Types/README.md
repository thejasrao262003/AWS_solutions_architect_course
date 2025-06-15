# AWS Storage Services Summary

## 🧱 Storage Types

| Type        | AWS Service | Notes                                  |
|-------------|-------------|----------------------------------------|
| Block       | EBS         | Attach to EC2 instances                |
| Object      | S3          | Highly durable, scalable object store |
| File        | EFS         | Linux-based shared file system        |
|             | FSx         | For Windows-based file system         |

---

## ☁️ AWS S3 Overview

- **Amazon S3** is an object storage service with:
  - High scalability and durability (99.99%)
  - Data replicated in at least 3 AZs
  - Max object size: 5TB
  - Common use cases: websites, data lakes, backups, app data

### 📜 S3 Bucket Policy Example

```json
{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Principal": "*",
        "Action": ["s3:ListBucket", "s3:GetObject"],
        "Resource": [
            "arn:aws:s3:::geeks2024",
            "arn:aws:s3:::geeks2024/*"
        ]
    }]
}
```

### 🔗 File URL Format

```
https://{bucket_name}.s3.{region}.amazonaws.com/{key}
```

---

## 💾 S3 Storage Classes and Pricing

| Storage Class             | Price ($/GB/month) | Use Case                                 |
|--------------------------|--------------------|-------------------------------------------|
| S3 Standard              | 0.023              | Frequent access                          |
| S3 Standard - IA         | 0.0125             | Infrequent access                        |
| S3 One Zone - IA         | 0.01               | Infrequent, one AZ only                  |
| Glacier Instant          | 0.004              | Archival, milliseconds retrieval         |
| Glacier Flexible         | 0.0036             | Archival, minutes to hours               |
| Glacier Deep Archive     | 0.00099            | Archival, 5 to 48 hours                  |
| Intelligent Tiering      | Dynamic            | Unknown access pattern, ML-managed       |
| S3 Express One Zone      | -                  | Ultra-low latency (ms) in one zone       |

📌 Intelligent Tiering adds a monitoring charge of **0.0025$/1000 objects** and requires object size > 128KB.

---

## 🚀 S3 Features

### 🔄 Versioning

- Maintains multiple versions of an object.
- Paid feature, works like Git for objects.

### 🗂️ Lifecycle Policies

- Define rules to transition or expire objects.
- Example: move to Glacier after 30 days, delete after 180 days.

### ⏫ Transfer Acceleration

- Uses nearest **Edge Location** for faster global upload.
- Transfers via AWS backbone.

### 🧩 S3 Access Points

- Enable granular access control with custom policies.
- Overcomes 20KB bucket policy limit.
- 1000 access points allowed per region.

---

## 🛠️ Multipart Upload

- Required for uploading objects > 5GB
- Only supported via AWS CLI/SDK (not console)

---

## 🚚 AWS Data Migration

### Offline (via AWS Snow Family):

| Device       | Capacity       | Notes                                |
|--------------|----------------|--------------------------------------|
| Snowcone     | 8TB HDD, 14TB SSD | Small-scale                         |
| Snowball     | 42–80 TB        | Compute or Storage optimized         |
| Snowmobile   | 100 PB          | Truck-sized for massive data loads   |

### Online (via AWS Storage Gateway):

- Bridge between on-prem and AWS
- Types:
  - **S3 File Gateway**
  - **FSx File Gateway**
  - **Tape Gateway**
  - **Volume Gateway**