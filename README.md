# terraform-eks-cicd
Certainly! Here's the revised version written in a more polished manner:

---

# EKS Deployment and CI/CD with Jenkins and Terraform

## Overview
This project automates the deployment of an Amazon EKS cluster and a containerized Nginx application using Terraform and Jenkins. The CI/CD pipeline ensures efficient infrastructure provisioning and application deployment.

## Project Workflow

### 1. Jenkins Server Setup
- Deploy an EC2 instance using Terraform.
- Install necessary tools: Java, Jenkins, AWS CLI, Terraform, Docker, SonarQube, Helm, Trivy, and Kubectl.
- Configure Jenkins and securely store AWS credentials.

### 2. EKS Cluster Setup
- Create an EKS cluster in a private subnet using Terraform.
- Use Terraform modules to manage VPC, security groups, and EKS.

### 3. Deploying Nginx Application
- Define Kubernetes manifests (Deployment & Service YAMLs).
- Deploy the Nginx application via Jenkins pipeline.

### 4. Jenkins CI/CD Pipeline
- Automate Terraform initialization, validation, planning, and applying.
- Configure user permissions to access the EKS cluster.
- Deploy Kubernetes manifests using `kubectl`.

### 5. Teardown & Cleanup
- Destroy the EKS cluster and resources using Jenkins pipeline.
- Manually delete any residual AWS resources if needed.

## Prerequisites
- AWS Account (IAM user with access key & secret key)
- Terraform CLI & AWS CLI installed
- Jenkins installed on an EC2 instance

## Deployment Instructions

1. **Clone the repository:**
    ```sh
    git clone https://github.com/vishal2505/terraform-eks-cicd.git
    ```
2. **Navigate to the Terraform directory:**
    ```sh
    cd terraform-eks-cicd/tf-aws-eks
    ```
3. **Initialize Terraform:**
    ```sh
    terraform init
    ```
4. **Validate Terraform configuration:**
    ```sh
    terraform validate
    ```
5. **Plan the Terraform deployment:**
    ```sh
    terraform plan -var-file=variables/dev.tfvars
    ```
6. **Apply the Terraform deployment:**
    ```sh
    terraform apply -var-file=variables/dev.tfvars -auto-approve
    ```
7. **Update kubeconfig to interact with the cluster:**
    ```sh
    aws eks update-kubeconfig --name my-eks-cluster
    ```
8. **Deploy the application:**
    ```sh
    kubectl apply -f manifest/deployment.yaml
    kubectl apply -f manifest/service.yaml
    ```
9. **Retrieve the LoadBalancer URL and access the application:**
    ```sh
    kubectl get svc nginx -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'
    ```
10. **Teardown resources when not needed:**
    ```sh
    terraform destroy -var-file=variables/dev.tfvars -auto-approve
    ```

## Improvements & Next Steps
- Enhance the CI/CD pipeline with automated testing and monitoring.
- Implement security best practices (RBAC, secrets management).
- Integrate observability tools like Prometheus & Grafana.

---

This project serves as a foundation for scalable Kubernetes deployments using Terraform and Jenkins!
