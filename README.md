# setting-up-vpc
# AWS VPC Setup - KCVPC

## Overview
This project sets up a Virtual Private Cloud (VPC) in the AWS EU-West-1 (Ireland) region. It includes a public and a private subnet, routing configurations, security measures, and deployment of EC2 instances.

---

## Architecture Diagram
[Insert Excalidraw diagram link or image here]

---

## Components and Configuration

### 1. **VPC Creation**
- **Name:** KCVPC
- **CIDR Block:** 10.0.0.0/16

### 2. **Subnets**
- **PublicSubnet (10.0.1.0/24)**
- **PrivateSubnet (10.0.2.0/24)**

### 3. **Internet Gateway**
- Created and attached to `KCVPC`.

### 4. **Route Tables**
- **Public Route Table:** Routes internet traffic (0.0.0.0/0) through IGW.
- **Private Route Table:** Routes internet traffic (0.0.0.0/0) through NAT Gateway.

### 5. **NAT Gateway**
- Created in `PublicSubnet` with an Elastic IP.
- Allows private instances to access the internet.

### 6. **Security Groups**
#### **PublicSG (For Public Instances)**
- Allow HTTP (80) and HTTPS (443) from anywhere.
- Allow SSH (22) from a specific IP.

#### **PrivateSG (For Private Instances)**
- Allow MySQL (3306) access from `PublicSubnet`.

### 7. **Network ACLs**
- **PublicNACL:** Allows HTTP, HTTPS, and SSH.
- **PrivateNACL:** Allows traffic from `PublicSubnet` and outbound internet access.

### 8. **EC2 Instances**
- **Public Instance:** Deployed in `PublicSubnet`, accessible via SSH.
- **Private Instance:** Deployed in `PrivateSubnet`, can access the internet through NAT.

---

## **Deployment Steps with Screenshots**

### 1. **Create the VPC**
- Navigate to AWS Console → VPC → Create VPC.
- Set **Name:** KCVPC, **CIDR Block:** 10.0.0.0/16.
- Click **Create**.

![VPC Screenshot](insert_link_here)

### 2. **Create Public and Private Subnets**
- Navigate to **Subnets** → **Create Subnet**.
- Select **VPC: KCVPC**.
- **PublicSubnet:** 10.0.1.0/24, **Availability Zone:** eu-west-1a.
- **PrivateSubnet:** 10.0.2.0/24, **Availability Zone:** eu-west-1a.
- Click **Create**.

![Subnets Screenshot](insert_link_here)

### 3. **Attach Internet Gateway**
- Navigate to **Internet Gateway** → **Create IGW**.
- Name it **KCVPC-IGW**.
- Attach it to **KCVPC**.

![IGW Screenshot](insert_link_here)

### 4. **Configure Route Tables**
#### Public Route Table
- Create **PublicRouteTable** and associate **PublicSubnet**.
- Add a route: **0.0.0.0/0 → IGW**.

#### Private Route Table
- Create **PrivateRouteTable** and associate **PrivateSubnet**.
- Add a route: **0.0.0.0/0 → NAT Gateway**.

![Route Tables Screenshot](insert_link_here)

### 5. **Create and Attach NAT Gateway**
- Allocate an **Elastic IP**.
- Create **NAT Gateway** in **PublicSubnet**.
- Attach the **Elastic IP**.

![NAT Gateway Screenshot](insert_link_here)

### 6. **Configure Security Groups**
#### PublicSG
- Allow **HTTP (80), HTTPS (443)** from anywhere.
- Allow **SSH (22)** from your IP.

#### PrivateSG
- Allow **MySQL (3306)** from **PublicSubnet**.

![Security Groups Screenshot](insert_link_here)

### 7. **Configure Network ACLs**
- **PublicNACL:** Allow HTTP, HTTPS, and SSH.
- **PrivateNACL:** Allow traffic from PublicSubnet.

![NACL Screenshot](insert_link_here)

### 8. **Launch EC2 Instances**
#### Public EC2 Instance
- Launch an instance in **PublicSubnet** using **PublicSG**.
- Verify SSH access.

#### Private EC2 Instance
- Launch an instance in **PrivateSubnet** using **PrivateSG**.
- Verify NAT Gateway access.

![EC2 Screenshot](insert_link_here)

---

## **Conclusion**
This setup provides a secure and scalable AWS VPC with public and private subnets, routing, security, and internet access configurations. The project ensures best practices in cloud networking and security.
