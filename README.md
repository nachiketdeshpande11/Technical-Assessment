# AWS Cloud Assignment – README.md

## 📌 **Task 1: Networking & Subnetting (AWS VPC Setup)**

### ✅ **VPC & Subnet Design Explanation**

A custom VPC was created using **CIDR 10.0.0.0/16**, providing a large address space suitable for multi-tier cloud environments. Two public and two private subnets were created across different Availability Zones to ensure high availability. An **Internet Gateway (IGW)** enables internet access for resources in public subnets, while a **NAT Gateway** placed in a public subnet allows private subnet instances to securely access the internet without exposing them.

Separate route tables were configured for public and private subnets to correctly manage traffic flow.

### 📍 **CIDR Ranges Used**

* **VPC:** `10.0.0.0/16`
* **Public Subnet 1:** `10.0.1.0/24`
* **Public Subnet 2:** `10.0.2.0/24`
* **Private Subnet 1:** `10.0.3.0/24`
* **Private Subnet 2:** `10.0.4.0/24`

Each `/24` subnet provides 256 IP addresses, suitable for scalable lab or demo environments.

### 📸 **Required Screenshots**

* VPC
* Subnets
* Route Tables
* NAT Gateway + Internet Gateway

---

## 📌 **Task 2: EC2 Static Website Hosting**

### ✅ **Instance Setup & Nginx Explanation**

A Free Tier **t2.micro** EC2 instance was launched inside a public subnet with auto-assigned public IP enabled. After SSH access, Nginx was installed to host a static website.

#### Commands Used

```sh
yum update -y
yum install nginx -y
systemctl start nginx
systemctl enable nginx
```

---

## 📌 **Task 3: High Availability + Auto Scaling**

### ✅ **Brief Explanation**

For high availability, EC2 application servers were deployed in **private subnets**, behind an **Application Load Balancer (ALB)** in public subnets. The ALB forwards traffic to a **Target Group** linked with an **Auto Scaling Group (ASG)** that spans multiple Availability Zones.

The ASG automatically creates, replaces, or scales instances based on demand or health checks.

**Traffic Flow:**
**Client → Public Subnet → ALB → Target Group → EC2 Instances (Private Subnets)**

### 📸 Required Screenshots

* ALB configuration
* Target Group
* Auto Scaling Group
* EC2 instances launched via ASG

---

## 📌 **Task 4: Billing & Free Tier Cost Monitoring**

### ✅ **Why Cost Monitoring Is Important**

AWS billing can quickly increase when unused resources are left running. Setting up cost alerts helps users stay within Free Tier limits and avoid unexpected charges.

### ✅ **Causes of Sudden AWS Bill Increases**

* EC2 instances running 24/7
* NAT Gateway hourly + data processing charges
* Active load balancers
* High data transfer costs
* CloudWatch logs and metrics ingestion
* Unused EBS volumes and snapshots
* Services not covered under Free Tier

### 📸 Required Screenshots

* CloudWatch Billing Alarm (₹100 threshold)
* Free Tier Usage Alerts (Billing Preferences)

---

## 📌 **Task 5: AWS Architecture Diagram (draw.io)**

### 🎯 Architecture Scenario

Designing a scalable AWS web application capable of handling **10,000+ concurrent users**.

### ✅ **Brief Explanation**

The architecture uses an Internet-facing **Application Load Balancer** to distribute traffic across an **Auto Scaling Group** of EC2 instances deployed in private subnets. The VPC includes separate public, private application, and private database subnets. An **Aurora database cluster** ensures high availability, while **ElastiCache Redis** improves application performance through caching.

Security is enforced using **Security Groups, Network ACLs, and AWS WAF**. **CloudWatch and CloudTrail** provide monitoring, logging, and operational insights. NAT Gateways allow secure outbound connectivity from private instances.

### 🧩 **Components Included**

1. Application Load Balancer (ALB)
2. Auto Scaling Group (ASG)
3. Public and Private Subnets
4. Aurora/RDS Database
5. ElastiCache (Redis)
6. Security Groups, NACLs, AWS WAF
7. CloudWatch & CloudTrail
8. NAT Gateway + Internet Gateway
