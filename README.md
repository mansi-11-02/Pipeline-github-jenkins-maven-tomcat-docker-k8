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

<img src="https://github.com/user-attachments/assets/11dcf2bb-2057-48ae-9406-a855381b0e81" alt="Description" style="border: 2px solid black;"/>

### 1. Source Code Management: 
Installing git in developer-server for local version control system.

![image](https://github.com/user-attachments/assets/d989e6f5-3ca8-4ea9-b523-c17f45ba2934)

Generating ssh-key to connect local server to our github account.

![image](https://github.com/user-attachments/assets/e4861203-2b18-431e-b7e9-bf9e9e305372)

![image](https://github.com/user-attachments/assets/e832ee35-fa7a-4c7d-898d-a133e79477f2)

Cloning java project files on local server

!image{: style="border: 1px solid #000;"}(https://github.com/user-attachments/assets/fd5ccc5c-f1fc-4e40-bcf1-e99f73108d4c)

The files are added, commited and pushed in the github Repository by creating remote origin on main branch.

![image](https://github.com/user-attachments/assets/b331807a-5550-4372-bdbc-22fcd2c92785)

The files are successfully pushed in the git repository.

![image](https://github.com/user-attachments/assets/840d3e82-df94-450a-b8da-6c57cfc44a99)

### 2. Build: Jenkins uses Maven plugin to build the Java application on tomcat server.
Download java, Jenkins and maven plugin on Jenkins-server. Starting Jenkins

![image](https://github.com/user-attachments/assets/21e17173-d968-44c4-b892-7d0b0cbe9be9)

![image](https://github.com/user-attachments/assets/63cd54e3-6680-4a23-afdc-54793af87c83)

Copy the public IP of your Jenkins server, allow port 8080 in the security group, and access it via http://<public-ip>:8080 in your web browser

![image](https://github.com/user-attachments/assets/1ea5905c-5c07-4398-bad4-33f24a8931a5)

Installing default packages.

![image](https://github.com/user-attachments/assets/ae522918-1198-4df9-a6c1-d74819ccd7ed)

![image](https://github.com/user-attachments/assets/64150dc8-c24c-44ce-bdde-6e0683157321)

Connecting Jenkins with github by creating webhook in github repository settings.
In webhook the secret is pasted from Jenkins by generating tokens.

![image](https://github.com/user-attachments/assets/3a0ed4d8-198b-429d-ac98-83173d934a48)

In Jenkins> dashboard > manage Jenkins > available plugins > maven integration >install

![image](https://github.com/user-attachments/assets/8aa70c23-8648-48b3-80c6-13cb22e8b6fe)

In installed plugins > type github > disable github branch source plugin and enable github plugin.

![image](https://github.com/user-attachments/assets/ac4bcca0-4f0c-4c18-8c9a-11fbeac17f20)

After installing restart Jenkins

![image](https://github.com/user-attachments/assets/ad8d35b7-bab9-4287-9de7-961433f68871)

In Manage Jenkins add tools and paste the java and maven path from Jenkins-server







