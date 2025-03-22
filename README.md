# End-to-End CI/CD Pipeline Documentation

This document provides a step-by-step guide to creating a CI/CD pipeline using Jenkins, GitHub, Maven, Docker, Amazon ECR, and Kubernetes. The pipeline will automate the process of building, testing, and deploying a sample Java web application.

## Problem Statement

Create an end-to-end CI/CD pipeline in AWS platform using Jenkins as the orchestration tool, GitHub as the SCM, Maven as the Build tool, deploy in a Docker instance and create a Docker image, store the Docker image in ECR, and achieve Kubernetes deployment using the ECR image. Build a sample Java web app using Maven.

## Architecture Overview

The CI/CD pipeline consists of the following stages:
1. **Source Code Management**: Java Code is stored in a GitHub repository.
2. **Build**: Jenkins uses Maven plugin to build the Java application on a Tomcat server.
3. **Dockerization**: The application is packaged into a Docker image.
4. **Image Storage**: The Docker image is stored in Amazon ECR.
5. **Deployment**: The Docker image is deployed to a Kubernetes cluster.

## Prerequisites

- AWS account
- GitHub account
- Jenkins server
- Docker installed on the Jenkins server
- Kubernetes cluster
- Maven installed on the Jenkins server
- AWS CLI configured with appropriate permissions

## Setup Instructions

### 1. Create EC2 Instances

Create 5 EC2 instances in AWS with the same security group, key-pair, and region.
