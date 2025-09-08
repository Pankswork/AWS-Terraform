# Terraform AWS Infrastructure Project

##  Project Overview

This project demonstrates how to use **Terraform** to build and manage AWS infrastructure as **Infrastructure as Code (IaC)**. The configuration provisions a complete environment that includes:

* A **VPC** with subnets and routing.
* An **Internet Gateway** and Route Table associations.
* A **Security Group** for HTTP and SSH access.
* Two **EC2 instances** running a web application (via user data).
* An **Application Load Balancer (ALB)** to distribute traffic.
* An **S3 bucket** for storage.

The project follows IaC best practices and is fully reproducible by running a few Terraform commands.

---

##  Infrastructure Components

### 1. **Networking**

* **VPC** – A custom Virtual Private Cloud.
* **Subnets** – Two public subnets across different Availability Zones (`us-east-1a`, `us-east-1b`).
* **Internet Gateway (IGW)** – Provides internet access to the VPC.
* **Route Table** – Routes traffic through the IGW.

### 2. **Security**

* **Security Group** allows:

  * **HTTP (port 80)** inbound from anywhere.
  * **SSH (port 22)** inbound from anywhere.
  * **All outbound traffic**.

### 3. **Compute**

* **EC2 Instances** – Two web servers (`t3.micro`) launched in each subnet.
* **User Data Scripts** – Installed via `userdata.sh` and `userdata1.sh`.

### 4. **Load Balancer**

* **Application Load Balancer (ALB)** distributes traffic across both EC2 instances.
* **Target Group** – Contains the EC2 instances.
* **Listener (port 80)** – Forwards requests to the target group.

### 5. **Storage**

* **S3 Bucket** – Simple storage service bucket created with a unique name.

### 6. **Outputs**

* **ALB DNS Name** – The public DNS name of the load balancer, which can be used to access the deployed application.

---

## How to Run

### 1. **Clone the Repository**

```bash
git clone <your-repo-url>
cd AWS-Terraform
```

### 2. **Initialize Terraform**

```bash
terraform init
```

### 3. **Validate Configuration**

```bash
terraform validate
```

### 4. **Format Code (Optional)**

```bash
terraform fmt
```

### 5. **Plan Infrastructure**

```bash
terraform plan
```

### 6. **Apply Changes**

```bash
terraform apply
```

(Type `yes` when prompted)

### 7. **Access the Application**

* After apply, Terraform outputs the **Load Balancer DNS**.
* Open it in a browser to test the setup.

### 8. **Destroy Infrastructure** (to avoid AWS charges)

```bash
terraform destroy
```

---

## Files in the Repo

* **main.tf** → Main Terraform configuration.
* **variable.tf** → Variables definition (if used).
* **userdata.sh / userdata1.sh** → Bootstrap scripts for EC2 instances.
* **terraform.tfstate** → State file (should not be committed to Git).


