# Sports API Management System

## Project Overview
This project demonstrates the creation of a **containerized API management system** for querying real-time sports data using the [SerpAPI](https://serpapi.com/). It utilizes **Amazon ECS (Fargate)** for running containers, **Amazon API Gateway** for exposing REST endpoints, and SerpAPI for fetching sports-related data. The system highlights advanced cloud practices, including **API management**, **container orchestration**, and **secure AWS integrations**.

---

## Features
- Exposes a **REST API** for querying real-time sports data via [SerpAPI](https://serpapi.com/).
- Runs a **containerized backend** using Amazon ECS with Fargate.
- Scalable and serverless architecture.
- **API management and routing** through Amazon API Gateway.

---

## Prerequisites
1. **SerpAPI Key**: Obtain your API key at [SerpAPI](https://serpapi.com/).
2. **AWS Account**: Create and configure an AWS account.
3. **AWS CLI**: Install and configure the AWS CLI for programmatic access.
4. **Docker**: Install Docker CLI and Desktop to build and push container images.

---

## Technical Architecture
![Technical Architecture](Screenshot%20(2).png)

---
## Features
- **Cloud Provider**: AWS
- **Core Services**: Amazon ECS (Fargate), API Gateway, CloudWatch, Amazon ECR
- **Programming Language**: Python 3.x
- **Containerization**: Docker
- **IAM Security**: Custom least privilege policies for ECS task execution and API Gateway
---
## Project Structure
```plaintext
sports-api-management/
├── flask_app.py              # Flask application for querying sports data
├── Dockerfile          # Dockerfile to containerize the Flask app
├── requirements.txt    # Python dependencies
├── .gitignore
└── README.md           # Project documentation
```

---

## Setup Instructions

### Clone the Repository
Clone the project repository:
```bash
git clone https://github.com/Tahseenullahihsan/30-Day-Devops-Challenge.git
cd 30-Day-Devops-Challenge/day04/sports-api-management
```

### Create ECR Repository
```bash
aws ecr create-repository --repository-name sports-api --region us-east-1
```

### Authenticate, Build, and Push the Docker Image
```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com

docker build --platform linux/amd64 -t sports-api .
docker tag sports-api:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:sports-api-latest
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:sports-api-latest
```

### Set Up ECS Cluster with Fargate

1. **Create an ECS Cluster**:
   - Navigate to the **ECS Console** → Clusters → Create Cluster.
   - Name your cluster `sports-api-cluster`.
   - Select **Fargate** as the infrastructure type, then create the cluster.

2. **Create a Task Definition**:
   - Navigate to **Task Definitions** → Create New Task Definition.
   - Name your task definition `sports-api-task`.
   - Select **Fargate** as the infrastructure type.
   - Add a container:
     - Name: `sports-api-container`
     - Image URI: `<AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:sports-api-latest`
     - Port: `8000` (Protocol: TCP)

3. **Define Environment Variables**:
   - Key: `SERP_API_KEY`
   - Value: `<YOUR_SERPAPI_KEY>`

4. **Run the Service with an ALB**:
   - Navigate to **Clusters** → Select Cluster → Service → Create Service.
   - Capacity Provider: Fargate.
   - Task Definition Family: `sports-api-task`.
   - Name your service: `sports-api-service`.
   - Desired Tasks: 2.

5. **Networking Configuration**:
   - Create a new **Security Group** with the following rules:
     - Type: **All TCP**
     - Source: Anywhere
   - Load Balancing:
     - Create a new **Application Load Balancer (ALB)**.
     - ALB Name: `sports-api-alb`.
     - Target Group Health Check Path: `/sports`.

6. **Test the ALB**:
   - After deployment, access the ALB DNS (e.g., `http://sports-api-alb-<AWS_ACCOUNT_ID>.us-east-1.elb.amazonaws.com/sports`) to confirm the API is functional.

---

### Configure API Gateway

1. **Create a New REST API**:
   - Go to the **API Gateway Console** → Create API → REST API.
   - Name the API: `Sports API Gateway`.

2. **Set Up Integration**:
   - Create a resource `/sports`.
   - Add a **GET Method**.
   - Integration Type: HTTP Proxy.
   - Target: ALB DNS (e.g., `http://sports-api-alb-<AWS_ACCOUNT_ID>.us-east-1.amazonaws.com/sports`).

3. **Deploy the API**:
   - Deploy the API to a stage (e.g., `Dev`).
   - Note the endpoint URL.

4. **Test the System**:
   - Use curl or a browser to test the endpoint:
     ```bash
     curl https://<api-gateway-id>.execute-api.us-east-1.amazonaws.com/Dev/sports
     ```

---

## What We Learned
- Setting up a **scalable, containerized application** with ECS.
- Creating public APIs using **API Gateway**.
- Integrating the **SerpAPI** securely with AWS.

---
---
 Contributions and feedback are welcome! 🎉
```

Let me know if any further modifications are required!