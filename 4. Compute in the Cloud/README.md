# ☁️ AWS Compute Services – Summary Notes

This document covers key insights from the **AWS Compute Services** module, focused on EC2 and Lambda. Ideal for quick revision and interview prep.

---

## 🔹 What is AWS EC2?

- EC2 is a secure, resizable compute capacity service in the cloud.
- Offers scalable, reliable infrastructure with minimal setup time.
- Provides flexibility in performance and cost optimization.

---

## 🔸 EC2 Instance Launch Considerations

1. **Name & Tags:** Use key-value pairs to manage and identify resources.
2. **Application & OS Image:** Choose your desired OS and prebuilt packages.
3. **Instance Type & Size:** Select based on workload.
    - **General Purpose (t, m)** – Balanced CPU & memory
    - **Storage Optimized (i)** – Frequent read/write (e.g., warehouses)
    - **Compute Optimized (c)** – High CPU workloads
    - **Memory Optimized (r)** – Fast memory tasks
    - **Accelerated Computing (g)** – GPU intensive
    - _e.g._: `c5g.xlarge` → Compute optimized, Graviton, large size
4. **Key Pair:** Used for SSH (PEM file). RSA public/private key-based.
5. **Networking & Security:** Choose VPC, subnet, IP, and security groups.
6. **Storage Options:**
    - **EBS – Elastic Block Storage**
        - HDD: Cold HDD, Throughput-optimized
        - SSD: `gp1`, `gp2`, `io1`, `io2`
7. **Placement & Tenancy:**
    - Shared vs Dedicated Instances vs Dedicated Hosts
8. **Placement Groups:**
    - **Cluster:** Low-latency node-to-node (e.g., HPC)
    - **Partition:** Isolated hardware per group (e.g., Kafka, Hadoop)
    - **Spread:** Reduces correlated failures
9. **Scripts & Metadata:**
    - Add bootstrap commands like `yum install httpd -y`
    - Metadata = runtime info (public IP, private IP, etc.)

---

## 💵 EC2 Pricing Options

| Option          | Discount     | Flexibility                              |
|-----------------|--------------|-------------------------------------------|
| On Demand       | ❌ None       | ✅ No commitment                          |
| Savings Plan    | ✅ Up to 72% | ✅ 1–3 year commitment (EC2/Compute Plans) |
| Spot Instances  | ✅ Up to 90% | ❌ Interruption-prone, bid-based           |
| Reserved        | ✅ 66–70%    | ❌ Standard (no changes), ✅ Convertible    |

---

## ⚡ AWS Lambda – Serverless Computing

- Run code without managing servers.
- Fully managed compute service with **auto-scaling**, **auto-patching**, and **auto-provisioning**.
- Ideal for event-driven architecture (e.g., S3 trigger, API Gateway).
- Use case example: See `lambda.png` for reference.

---