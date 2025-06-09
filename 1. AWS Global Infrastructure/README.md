# AWS Solutions Architect - Module 1 Summary

This document summarizes the key concepts covered in Module 1 of the AWS Solutions Architect course.

---

## Class 1: AWS Global Infrastructure

### What is Cloud Computing?

- Access services on demand  
- Avoid large upfront investments  
- Provision computing resources as needed  
- Pay only for what you use  

### AWS Data Centers, Regions, and Availability Zones

#### AWS Regions:
- As of today, AWS is present in 33 regions.
- Examples:
  - 4 in the US
  - 2 in India
  - 2 in Australia

#### AWS Data Centers:
- AWS services operate within data centers.
- Data centers host thousands of AWS services and servers.
- All data centers use AWS backbone network equipment.
- Data centers are organized into Availability Zones.

#### Availability Zones:
- Regions: 33
- Example: Australia (Sydney)
  - Availability Zones: AZ1, AZ2, AZ3
  - Each AZ contains multiple data centers.

> Refer to images: `availability_zones.png` and `us-east-1.png` for visualization.

---

## Class 2: Local Zones, Wavelength Zones, and Edge Locations

### Low Latency Infrastructure

#### Local Zones:
- Problem: Sticking to only AZs can cause latency for users far from the region.
- Example: Region in Mumbai but users in Gurgaon.
- Solution: Local Zones — small data centers with limited services like EC2, VPC, RDS, ECS, EKS, etc.
  - Existing: Delhi, Kolkata
  - Coming Soon: Chennai, Bangalore

#### Wavelength Zones:
- Provide ultra-low latency to mobile devices and users.
- Example Applications: Autonomous vehicles, medical image screening.
- Traditional flow: Client → Mobile Tower → CSP → AWS Region (90–180ms latency)
- Wavelength flow: Client → Mobile Tower → CSP → Wavelength Zone (significantly lower latency)

#### Edge Locations:
- Caching sites for fast content retrieval.
- Used by services like CloudFront.
- Low latency but may not always have the latest data.

---

## Class 3: AWS Well-Architected Framework

### 6 Pillars of the Framework

Use the acronym **C.R.O.P.S.S** to remember:

- **C** - **Cost Optimized**
  - Analyze expenditure
  - Use cost-effective resources
  - Avoid guessing

- **R** - **Reliability**
  - Recover from failures or disasters
  - Regularly test recovery procedures

- **O** - **Operational Excellence**
  - Perform operations as code
  - Eliminate human errors

- **P** - **Performance Efficiency**
  - Reduce latency
  - Use serverless architecture
  - Monitor resources and applications

- **S** - **Security**
  - Principle of least privilege
  - Use Multi-Factor Authentication (MFA)

- **S** - **Sustainability**
  - Minimize environmental impact
  - Maximize resource utilization

### Purpose of the Framework:
- Helps build secure, high-performing, resilient, and efficient cloud architectures.
- Provides a consistent methodology for evaluating and improving architectures.

---

*End of Module 1 Summary*
