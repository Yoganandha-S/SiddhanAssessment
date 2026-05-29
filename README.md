# Cloud Engineer Assessment

## Project Overview

This project demonstrates a production-like deployment of a containerized web application using Infrastructure as Code, CI/CD automation, monitoring, and AWS cloud services.

The application consists of two Docker containers running on a single EC2 instance and deployed automatically using GitHub Actions.

---

## Architecture Components

* AWS VPC
* Public and Private Subnets
* Internet Gateway
* Security Groups
* EC2 Instance
* Docker Containers
* GitHub Actions Self-Hosted Runner
* CloudWatch Agent Monitoring
* Terraform Infrastructure Provisioning

---

## Repository Structure

```text
.
├── app/
│   ├── server1/
│   └── server2/
│
├── terraform/
│   └── main.tf
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
└── README.md
```

---

# Deployment Steps

## Step 1: Infrastructure Provisioning

Provision infrastructure using Terraform.

Commands:

```bash
terraform init
terraform validate
terraform plan
terraform apply
```

Terraform provisions:

* VPC
* 2 Public Subnets
* 2 Private Subnets
* Internet Gateway
* Route Tables
* Security Groups
* EC2 Instance

---

## Step 2: Configure EC2

SSH into EC2:

```bash
ssh -i runbook.pem ec2-user@<public-ip>
```

Install Docker:

```bash
sudo yum install docker -y
sudo systemctl enable docker
sudo systemctl start docker
```

---

## Step 3: Configure Self Hosted Runner

Create and configure GitHub self-hosted runner on EC2.

Install service:

```bash
sudo ./svc.sh install
sudo ./svc.sh start
```

Validate:

```bash
sudo ./svc.sh status
```

---

## Step 4: Application Deployment

Two Docker applications were created:

Server 1:

```text
Hello from Server 1
```

Server 2:

```text
Hello from Server 2
```

Containers are deployed using:

```bash
docker run -d --name server1 -p 8080:80 server1

docker run -d --name server2 -p 8081:80 server2
```

---

## Step 5: CI/CD Pipeline

GitHub Actions workflow performs:

1. Checkout code
2. Build Docker images
3. Stop existing containers
4. Redeploy containers
5. Verify deployment

Trigger:

```text
Push to main branch
```

---

## Step 6: Monitoring

Monitoring implemented using CloudWatch Agent.

Collected Metrics:

* CPU Utilization
* Memory Utilization
* Disk Usage

CloudWatch namespace:

```text
CloudAssessment
```

---

# Design Decisions

* Terraform selected for Infrastructure as Code.
* Docker used for containerization.
* Self-hosted runner selected for deployment automation.
* Single EC2 used for cost optimization.
* Monitoring implemented using CloudWatch Agent.

---

# Trade-offs Considered

* Single EC2 instance used instead of multi-instance deployment to reduce cost.
* Public subnet deployment used for simplicity and budget constraints.
* Self-hosted runner colocated with application infrastructure.

---

# Cost Optimization Approach

* Used t3.micro instance.
* Single EC2 instance used.
* CloudWatch monitoring limited to essential metrics.
* Load balancer deployment deferred until final validation stage.
* Infrastructure destroyed after testing.

---

# Validation

Application Validation:

```text
http://<public-ip>:8080
http://<public-ip>:8081
```

Monitoring Validation:

```text
AWS CloudWatch Metrics
```

CI/CD Validation:

```text
GitHub Actions Pipeline Success
```
