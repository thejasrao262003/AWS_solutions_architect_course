# ✅ Module 3 – AWS Networking Essentials

This module covers the foundational concepts of networking within AWS. Topics include IP addressing, Virtual Private Cloud (VPC), subnets, routing, Elastic IPs, NAT gateways, Network Access Control Lists (NACLs), and Security Groups.

---

## 📘 Topics Covered

---

### 🔢 IP Addressing and CIDR

- `192.168.0.0/16` – CIDR notation specifies IP range and subnet mask.
- `/24` means **24 bits are fixed**, so we get `2^(32-24) = 256` IP addresses.
- In typical networks:  
  - `2` IPs are reserved:  
    - `192.168.0.0` (Network Address)  
    - `192.168.0.255` (Broadcast Address)  
  - Usable IPs = `2^(32-n) - 2`

- **In AWS**, 5 IPs are reserved:  
  - `.0` – Network Address  
  - `.1` – VPC Router  
  - `.2` – DNS  
  - `.3` – Future Use  
  - `.255` – Broadcast  
  - Usable IPs = `2^(32-n) - 5`

---

### 🌐 Virtual Private Cloud (VPC)

- A VPC is a **logically isolated network** in AWS.
- Analogy: Like buying a piece of land before building houses.
- **Subnets** divide the VPC:
  - **Public Subnet** – accessible via internet.
  - **Private Subnet** – isolated from public internet.

---

### 🚪 Internet Gateway & Route Table

- **Internet Gateway (IGW):** Enables communication between instances in the VPC and the internet.
- **Route Table:**
  - Public subnet route table:
    - Local route
    - `0.0.0.0/0` → IGW
  - Private subnet route table:
    - Local route only (unless using NAT Gateway)

---

### 📡 Elastic IP (EIP)

- Static public IP address allocated by AWS.
- Remains the same even after EC2 stop/start.
- **Note:** One EIP per running EC2 is free. Extra or unused EIPs incur cost.

---

### 🔁 NAT Gateway

- Allows **outbound internet access** for private instances.
- Placed in **public subnet** and associated with an EIP.
- **Route table** of private subnet must direct `0.0.0.0/0` → NAT Gateway.
- **Does not allow inbound internet traffic.**

---

### 🛡️ NACL (Network ACL)

- Subnet-level firewall.
- Stateless – return traffic must be explicitly allowed.
- Rules evaluated **in order** (lowest → highest number).
- Supports both `Allow` and `Deny`.

---

### 🔐 Security Group

- Instance-level firewall.
- Stateful – return traffic automatically allowed.
- Only `Allow` rules supported.
- All rules evaluated together.
- Common use: Allow SSH (22), HTTP (80), etc., per instance.

---

## 📚 Summary

| Component         | Scope        | Stateful | Supports Deny | Use Case                              |
|------------------|--------------|----------|---------------|----------------------------------------|
| Security Group    | EC2 Instance | ✅ Yes   | ❌ No          | Instance-level access control          |
| NACL              | Subnet       | ❌ No    | ✅ Yes         | Subnet-level access, IP-based blocking |
| NAT Gateway       | Private Subnet | ➖     | ➖             | Outbound internet for private EC2s     |
| Internet Gateway  | VPC          | ➖       | ➖             | Public access for public subnets       |

---

© Module 3 – AWS Networking. Happy Cloud Building ☁️🚀