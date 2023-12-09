# Robust CICD Pipeline for Java Application

**This project demonstrates how to create a robust CICD pipeline for a Java application using various tools and technologies. The pipeline automates the build, test, and deployment processes for the application and ensures the quality and reliability of the code.**

## Tools and Technologies

The following tools and technologies are used in this project:

- Terraform - To build the infrastructure
- Ansible - For configuration management
- Jenkins - To implement the CI/CD pipeline
- Maven - To build the application
- Docker - To containerize the application
- SonarQube - To perform static code analysis
- JFrog Artifactory - To store the build artifact
- Helm - Package the kubernetes manifests
- Kubernetes - Deploy the application


## Infrastructure Setup

The infrastructure is created using Terraform, which sets up a custom VPC on AWS with public subnets. Inside these subnets, three servers are hosted:
1. Ansible Server
2. Jenkins Master Server
3. Build Slave Server

Ansible acts as the configuration management tool for the Jenkins master and build slave servers, installing the required packages on these servers.

## CI/CD Pipeline

The Jenkins server connects with the build slave server to manage the build process for the application. The pipeline is integrated with GitHub webhooks, triggering automatically whenever code changes are pushed.

### Build Process

The pipeline starts with the build process using Maven, which also performs unit testing. The build process generates a JAR file as the artifact for the application.

### Static Code Analysis

The pipeline then performs static code analysis using SonarQube, checking the quality of the code. The pipeline passes only if the code meets the quality gates defined by SonarQube.

### Dockerization

The pipeline containerizes the artifact using Docker, creating a Docker image for the application. This Docker image is then pushed to JFrog Artifactory, which acts as a registry for storing the images.

### Deployment

The pipeline packages the Kubernetes manifests using Helm, creating a Helm chart for the application. This Helm chart is then used to deploy the application to an Elastic Kubernetes Service (EKS) cluster. The EKS cluster is created using eksctl and AWS CLI.

## Conclusion

This project successfully creates a robust and efficient CI/CD pipeline for a Java Spring Boot application, leveraging various DevOps tools and technologies.

