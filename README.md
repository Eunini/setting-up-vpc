# setting-up-vpc
# AWS VPC Setup - KCVPC

## Overview
This project sets up a Virtual Private Cloud (VPC) in the AWS EU-West-1 (Ireland) region. It includes a public and a private subnet, routing configurations, security measures, and deployment of EC2 instances.

---

## Architecture Diagram
![vpc setup-Page-1 drawio (1)](https://github.com/user-attachments/assets/399456a9-d79f-40d0-9c50-04e3ee56a4bf)



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

![VPC Screenshot]![vpc 1](https://github.com/user-attachments/assets/2deaa0ec-2ae3-48c7-a2bf-e4a3bec10df2)


### 2. **Create Public and Private Subnets**
- Navigate to **Subnets** → **Create Subnet**.
- Select **VPC: KCVPC**.
- **PublicSubnet:** 10.0.1.0/24, **Availability Zone:** eu-west-1a.
- **PrivateSubnet:** 10.0.2.0/24, **Availability Zone:** eu-west-1a.
- Click **Create**.

![Subnets Screenshot]![private edit subnet](https://github.com/user-attachments/assets/83a5413e-f0e3-4adc-b235-e1a38e05bd60)
![subnets](https://github.com/user-attachments/assets/8163748b-6cb8-4576-9ed9-a9dd890dc702)



### 3. **Attach Internet Gateway**
- Navigate to **Internet Gateway** → **Create IGW**.
- Name it **KCVPC-IGW**.
- Attach it to **KCVPC**.

![IGW Screenshot]![attached igw](https://github.com/user-attachments/assets/2b208c25-e834-42e2-89ec-f5b9869e1633)


### 4. **Configure Route Tables**
#### Public Route Table
- Create **PublicRouteTable** and associate **PublicSubnet**.
- Add a route: **0.0.0.0/0 → IGW**.

#### Private Route Table
- Create **PrivateRouteTable** and associate **PrivateSubnet**.
- Add a route: **0.0.0.0/0 → NAT Gateway**.

![Route Tables Screenshot![route table](https://github.com/user-attachments/assets/53ae02db-824c-4d53-8ecf-6dd479387c46)


### 5. **Create and Attach NAT Gateway**
- Allocate an **Elastic IP**.
- Create **NAT Gateway** in **PublicSubnet**.
- Attach the **Elastic IP**.

![NAT Gateway Screenshot]![nat gateway1](https://github.com/user-attachments/assets/21da9b9e-7498-4a16-aba6-d3d462f3848d)


### 6. **Configure Security Groups**
#### PublicSG
- Allow **HTTP (80), HTTPS (443)** from anywhere.
- Allow **SSH (22)** from your IP.

#### PrivateSG
- Allow **MySQL (3306)** from **PublicSubnet**.

![Security Groups Screenshot]![privateSG](https://github.com/user-attachments/assets/4c5a966c-05f5-4d09-9529-d5f9894d3712)
![publicSG](https://github.com/user-attachments/assets/0de72e46-12bf-432f-911e-1df4fb567e7e)


### 7. **Configure Network ACLs**
- **PublicNACL:** Allow HTTP, HTTPS, and SSH.
- **PrivateNACL:** Allow traffic from PublicSubnet.

![NACL Screenshot]![allocate elastic ip](https://github.com/user-attachments/assets/02bcd335-79b3-4ce1-affd-b1b9ed9fee40)
![add route-to-igw](https://github.com/user-attachments/assets/97305f2d-0770-4821-9b2e-cf03af6c59e0)


### 8. **Launch EC2 Instances**
#### Public EC2 Instance
- Launch an instance in **PublicSubnet** using **PublicSG**.
- Verify SSH access.

#### Private EC2 Instance
- Launch an instance in **PrivateSubnet** using **PrivateSG**.
- Verify NAT Gateway access.

![EC2 Screenshot]![private instance status](https://github.com/user-attachments/assets/99063075-758b-4a3f-b20b-00174703e304)
![public status pass](https://github.com/user-attachments/assets/7df69054-1a80-44ba-bb9b-c001a44a9275)


---

## **Conclusion**
This setup provides a secure and scalable AWS VPC with public and private subnets, routing, security, and internet access configurations. The project ensures best practices in cloud networking and security.
