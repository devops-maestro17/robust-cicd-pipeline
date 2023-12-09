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


## Pipeline Overview
The pipeline consists of the following steps:

- Build: The pipeline starts with the build process using Maven and performs unit testing. The build process generates a JAR file as the artifact for the application.

- Static Code Analysis: The pipeline performs static code analysis using SonarQube and checks the quality of the code. The pipeline passes only if the code meets the quality gates defined by SonarQube.

- Containerization: The pipeline containerizes the artifact using Docker and creates a Docker image for the application. The Docker image is then pushed to JFrog Artifactory, which acts as a registry for storing the images.

- Packaging: The pipeline packages the Kubernetes manifests using Helm and creates a Helm chart for the application. The Helm chart is then used to deploy the application to Elastic Kubernetes Service (EKS) cluster.

- Deployment: The pipeline deploys the application to EKS cluster using Helm. The pipeline verifies the status of the deployment and reports the success or failure of the pipeline.

- GitHub Webhook Integration: The pipeline is integrated with GitHub webhook, which allows the pipeline to be triggered automatically whenever any code changes are made to the GitHub repo. The webhook sends a notification to Jenkins, which then starts the pipeline execution. This ensures that the pipeline is always up to date with the latest code changes and the application is always in sync with the source code.

### Terraform is used to build the custom VPC with servers to host Ansible, Jenkins master and build slave on AWS. Ansible is used to manage the configuration on the Jenkins and build servers by installing required packages using Ansible playbooks.
