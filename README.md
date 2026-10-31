# AWS Highly Available Web Application Using Auto Scaling and Load Balancer

## 📌 Project Overview

This project demonstrates the design and implementation of a Highly Available Web Application using AWS services.

The objective is to build a scalable and fault-tolerant web application that can handle sudden traffic spikes during peak sales periods.

The architecture uses an Application Load Balancer (ALB) to distribute incoming traffic across multiple EC2 instances and an Auto Scaling Group (ASG) to automatically adjust the number of instances based on CPU utilization.

The application is deployed across two Availability Zones to improve availability and reduce downtime.

## 🎯 Project Objectives

- Design a highly available AWS architecture.
- Create a custom VPC with two public subnets.
- Deploy EC2 instances across multiple Availability Zones.
- Configure an Application Load Balancer.
- Implement an EC2 Auto Scaling Group.
- Configure CPU-based automatic scaling.
- Monitor infrastructure using Amazon CloudWatch.
- Test automatic instance replacement and load balancing.

### Architecture Workflow

1. Users send HTTP requests to the application.
2. Application Load Balancer receives incoming traffic.
3. ALB distributes traffic across healthy EC2 instances.
4. EC2 instances host the web application using Apache.
5. Auto Scaling Group maintains the desired instance capacity.
6. CloudWatch monitors CPU utilization.
7. Auto Scaling launches additional instances when demand increases.
8. Unhealthy instances are replaced automatically.

## 🛠️ Technologies Used

| AWS Service / Tool | Purpose |
|---|---|
| Amazon VPC | Network infrastructure |
| Amazon EC2 | Application hosting |
| Application Load Balancer | Traffic distribution |
| Auto Scaling Group | Automatic scaling |
| Launch Template | EC2 configuration |
| Target Group | Health checks |
| CloudWatch | Infrastructure monitoring |
| Amazon Linux 2023 | Operating system |
| Apache | Web server |
| Bash | Automation scripting |

## 🌐 AWS Infrastructure Configuration

| Component | Configuration |
|---|---|
| AWS Region | Asia Pacific (Mumbai) |
| VPC Name | HA-WebApp-VPC |
| VPC CIDR | 10.0.0.0/16 |
| Public Subnet 1 | 10.0.1.0/24 |
| Public Subnet 2 | 10.0.2.0/24 |
| Availability Zones | 2 |
| AMI | Amazon Linux 2023 |
| Instance Type | t2.micro / t3.micro |
| Minimum Instances | 2 |
| Desired Instances | 2 |
| Maximum Instances | 5 |
| Scaling Policy | Target Tracking |
| CPU Target | 50% |
| Health Check | ELB |

## ⚙️ Implementation Steps

### 1. Create Custom VPC

- Created a custom VPC with CIDR 10.0.0.0/16.
- Created two public subnets in different Availability Zones.
- Created and attached an Internet Gateway.
- Configured route tables.
- Enabled automatic public IP assignment.

### 2. Configure Security Groups

**ALB Security Group**
- HTTP (Port 80): Allow from 0.0.0.0/0.

**EC2 Security Group**
- HTTP (Port 80): Allow from ALB Security Group.
- SSH (Port 22): Allow from My IP only.

### 3. Create Launch Template

Created a Launch Template with:

- Amazon Linux 2023 AMI.
- EC2 instance type.
- Security Group.
- Key Pair.
- User Data script.

The User Data script automatically installs Apache and deploys the web application.

### 4. Create Target Group

- Target Type: Instances.
- Protocol: HTTP.
- Port: 80.
- Health Check Path: /
- Success Code: 200.

### 5. Configure Application Load Balancer

- Created an internet-facing Application Load Balancer.
- Selected two public subnets in different Availability Zones.
- Configured HTTP listener on port 80.
- Forwarded traffic to the Target Group.

### 6. Configure Auto Scaling Group

Created an Auto Scaling Group using the Launch Template.

Capacity configuration:

- Minimum Capacity: 2
- Desired Capacity: 2
- Maximum Capacity: 5

Attached the Target Group and enabled ELB health checks.

### 7. Configure Scaling Policy

Configured a Target Tracking Scaling Policy.

- Metric: Average CPU Utilization.
- Target Value: 50%.
- Instance Warmup: 120 seconds.

The Auto Scaling Group adjusts the number of EC2 instances based on CPU utilization.

## 🧪 Testing and Validation

### Test 1: Application Accessibility

Accessed the application using the ALB DNS name.

Expected Result: The application should load successfully.

### Test 2: Load Balancing

Sent multiple requests through the ALB and verified that traffic reached registered EC2 instances.

### Test 3: Instance Failure Testing

- Manually terminated one EC2 instance.
- Verified that Auto Scaling detected the reduced capacity.
- Observed automatic replacement instance launch.
- Verified application accessibility through ALB.

### Test 4: CPU Load Testing

Generated CPU load using the Linux stress utility.

```bash
sudo stress --cpu 2 --timeout 600
```

Monitored CPU utilization using CloudWatch and observed Auto Scaling activity.

### Test 5: Scale-In Testing

After CPU utilization decreased, observed the Auto Scaling Group scaling back toward the desired capacity.

## 📸 Project Screenshots

Add actual AWS console screenshots in the screenshots folder.

| Screenshot | Description |
|---|---|
| vpc.png | Custom VPC configuration |
| subnets.png | Multi-AZ public subnets |
| launch-template.png | Launch Template |
| target-group.png | Target Group health |
| alb.png | Application Load Balancer |
| autoscaling-group.png | Auto Scaling Group |
| scaling-policy.png | CPU scaling policy |
| cpu-load-test.png | CPU utilization |
| scaling-events.png | Scaling activity history |
| application.png | Running web application |

## 📂 Repository Structure

```text
AWS-Highly-Available-Web-Application/
│
├── README.md
│
├── architecture/
│   └── architecture.png
│
├── user-data/
│   └── userdata.sh
│
├── screenshots/
│   ├── vpc.png
│   ├── subnets.png
│   ├── launch-template.png
│   ├── target-group.png
│   ├── alb.png
│   ├── autoscaling-group.png
│   ├── scaling-policy.png
│   ├── cpu-load-test.png
│   ├── scaling-events.png
│   └── application.png
│
└── testing/
    └── testing-results.md
```

## 🔐 High Availability Strategy

This project improves application availability using:

- Multi-AZ deployment.
- Application Load Balancer.
- EC2 health checks.
- Auto Scaling Group.
- Automatic instance replacement.
- CPU-based scaling.
- CloudWatch monitoring.

Note: This implementation demonstrates application-tier high availability. Production environments may additionally require private subnets, NAT Gateway, HTTPS, database redundancy, and additional security controls.

## 📈 Project Outcomes

- Successfully designed a Multi-AZ AWS architecture.
- Implemented automatic EC2 provisioning.
- Configured traffic distribution using ALB.
- Implemented CPU-based Auto Scaling.
- Tested automatic instance replacement.
- Monitored infrastructure using CloudWatch.

## 🚀 Future Improvements

- Deploy EC2 instances in private subnets.
- Configure HTTPS using AWS Certificate Manager.
- Integrate Amazon RDS Multi-AZ.
- Configure CloudWatch alarms and notifications.
- Implement CI/CD using Jenkins.
- Automate infrastructure using Terraform.

## 👨‍💻 Skills Demonstrated

AWS | EC2 | VPC | Application Load Balancer | Auto Scaling Group | CloudWatch | Linux | Apache | Bash Scripting | High Availability | Load Balancing | Cloud Infrastructure

## 👤 Author

**Bhushan Jagtap**

Aspiring AWS Cloud / DevOps Engineer

- GitHub: https://github.com/Bhushan1814
- LinkedIn: https://www.linkedin.com/in/bhushansjagtap

---

⭐ If you find this project useful, feel free to star the repository!
