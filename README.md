# End-to-End CI/CD Pipeline Documentation

This document provides a step-by-step guide to creating a CI/CD pipeline using Jenkins, GitHub, Maven, Docker, Amazon ECR, and Kubernetes. The pipeline will automate the process of building, testing, and deploying a sample Java web application.

## Problem Statement

> **Create an end-to-end CI/CD pipeline in AWS platform using Jenkins as the orchestration tool, GitHub as the SCM, Maven as the Build tool, deploy in a Docker instance and create a Docker image, store the Docker image in ECR, and achieve Kubernetes deployment using the ECR image. Build a sample Java web app using Maven.**

## Architecture Overview

The CI/CD pipeline consists of the following stages:
1. **Source Code Management**: Java code is stored in a GitHub repository.
2. **Build**: Jenkins uses Maven plugin to build the Java application on a Tomcat server.
3. **Dockerization**: The application is packaged into a Docker image.
4. **Image Storage**: The Docker image is stored in Amazon ECR.
5. **Deployment**: The Docker image is deployed to a Kubernetes cluster.

## Steps to Create the CI/CD Pipeline

 
## Create 5 instances in AWS EC2 with the same security group, key-pair, and region.
![image](https://github.com/user-attachments/assets/11dcf2bb-2057-48ae-9406-a855381b0e81)
### 1.Source Code Management: 
#### Installing git in developer-server for local version control system.
Generating ssh-key to connect local server to our github account.

