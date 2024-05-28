**E-Cart Website DevOps Pipeline**

This project demonstrates a complete CI/CD pipeline for an eCart website using Jenkins. The pipeline includes OWASP Dependency Check, SonarQube analysis, artifact building and storage with Maven and Nexus, Docker image creation, and deployment to a Kubernetes cluster.

**Table of Content**s:

● Project Overview 

● Technologies Used

● CI/CD Pipeline

     1. SonarQube Analysis
      
     2. OWASP Dependency Check
      
     3. Build Artifacts with Maven
    
     4. Store Artifacts in Nexus
    
     5. Build Docker Image
       
     6. Deploy to Kubernetes
   
● Setup Instructions

     1 Prerequisites
   
     2 Jenkins Configuration
   
     3 Kubernetes Configuration

● Files in the Repository




※ Project Overview 

The eCart DevOps project demonstrates a complete CI/CD pipeline for an eCart web application. It uses Jenkins to automate the processes of code analysis, security checks, building, storing, containerizing, and deploying the application.

※ **Technologies Used**

    ● Jenkins: CI/CD automation server

    ● SonarQube: Static code analysis

    ● OWASP Dependency Check: Dependency vulnerability analysis

    ● Maven: Build automation tool for Java projects

    ● Nexus: Artifact repository manager

    ● Docker: Containerization platform

    ● Kubernetes: Container orchestration platform

※ **CI/CD Pipeline**

   1. SonarQube Analysis: 
Performs static code analysis to detect bugs, code smells, and security vulnerabilities.

   2. OWASP Dependency Check:  
Scans the project's dependencies for known vulnerabilities.

   4. Build Artifacts with Maven: 
Compiles the code, runs tests, and packages the application into an artifact (e.g., JAR file).

   5. Store Artifacts in Nexus: 
Uploads the built artifacts to a Nexus repository for storage and versioning.

   6. Build Docker Image: 
Creates a Docker image of the application using the built artifact and the provided Dockerfile.

   7. Deploy to Kubernetes: 
Deploys the Docker image to a Kubernetes cluster using the provided deployment and service files.

※ **Setup Instructions** 

**Prerequisites:** 

   1. Jenkins installed and configured

   2. SonarQube server set up

   3. Nexus repository set up

   4. Docker installed on Jenkins server

   5. Kubernetes cluster set up and configured

   6. Java and Maven installed

**Jenkins Configuration:** 

**1. Install Required Plugins:**

    SonarQube Scanner Plugin

    OWASP Dependency-Check Plugin

    Nexus Artifact Uploader Plugin

    Docker Pipeline Plugin

    Kubernetes Continuous Deploy Plugin

**2. Configure Global Tools:**

    JDK installation

    Maven installation

    SonarQube server details

    Docker installation

**3. Create Jenkins Pipeline:**

    Create a new pipeline job in Jenkins.

    Configure SCM to pull the repository containing the eCart project and Jenkinsfile.

**Kubernetes Configuration:**

    Ensure Kubernetes Cluster is Up and Running.

    Configure kubeconfig in Jenkins for cluster access.

※ **Files in the Repository**

   1. Jenkinsfile: Defines the CI/CD pipeline stages

   2. Dockerfile: Contains instructions to build the Docker image

   3. k8s-deployment.yml: Kubernetes deployment configuration

   4. k8s-service.yml: Kubernetes service configuration
