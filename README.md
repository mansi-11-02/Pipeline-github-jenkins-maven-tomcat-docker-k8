# End-to-End CI/CD Pipeline Documentation

This document provides a step-by-step guide to creating a CI/CD pipeline using Jenkins, GitHub, Maven, Docker, Amazon ECR, and Kubernetes. The pipeline will automate the process of building, testing, and deploying a sample Java web application.

<img src="https://github.com/user-attachments/assets/7c354bbf-b4dd-4b9b-8379-0b0d251cbac9" alt="Description" style="border: 2px solid black;"/>

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

![image](https://github.com/user-attachments/assets/11dcf2bb-2057-48ae-9406-a855381b0e81)

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
After installing restart Jenkins

![image](https://github.com/user-attachments/assets/ad8d35b7-bab9-4287-9de7-961433f68871)

In Manage Jenkins add tools and paste the java and maven path from Jenkins-server

![image](https://github.com/user-attachments/assets/40f813a5-bd78-4e8e-9361-4fc81aefaa75)

![image](https://github.com/user-attachments/assets/dde89b65-cb2d-44d6-a8b7-15529a821a31)

![image](https://github.com/user-attachments/assets/92fd126c-c832-4477-af54-405be3a0413e)

Create new item > type name > maven project

![image](https://github.com/user-attachments/assets/e5cd1ce8-f22c-4f30-8f1d-82b5c8571e65)

Add your git repository link

![image](https://github.com/user-attachments/assets/274dc7e1-70c6-4fd8-a231-e00a26e9462b)

Change branch to main.

![image](https://github.com/user-attachments/assets/0b264122-16d9-4a45-b824-7f25688b85c1)

Save, apply, and build now > The build should be successful.

![image](https://github.com/user-attachments/assets/489c86fa-4d2b-4e0f-a469-84f9699e7128)

Jenkins artifacts are visible, it means the build outputs or results are accessible.

![image](https://github.com/user-attachments/assets/abb1f090-a6c0-441b-aa5b-04b3925bc5cd)

Open tomcat-server in the terminal
Install java and apache tomcat in /opt directory

![image](https://github.com/user-attachments/assets/bff2232b-5f6d-4c37-816b-31d67ea89fae)

Unzip the apache tomcat folder. Enter in apache-tomcat folder. Open the bin file and find the path of all context.xml files.

![image](https://github.com/user-attachments/assets/d692fd9f-ab19-4b0d-be51-efdae489d1cc)

Change the last two files: comment valve statement in both the files <!-- -->

![image](https://github.com/user-attachments/assets/a6174270-ad33-4da6-a4bf-1fbdf96cf6fe)

Open the conf/ tomcat-users.xml file and add users:

![image](https://github.com/user-attachments/assets/9151d66e-cf8a-434d-bb2a-342d0adf7bed)

Starting tomcat

![image](https://github.com/user-attachments/assets/a7bfbc23-5b13-47c4-a953-cddfaf688d56)

Go to Jenkins in web browser:
To integrate tomat server with Jenkins:
Go to Manage Jenkins > plugin > available plugins > deploy to container > install
Manage Jenkins > Credentials > system > global credentials > add
   Username: developer
   Password: developer
   Id: tomcat-cred

![image](https://github.com/user-attachments/assets/197cbeb1-c447-4c2c-9c46-ab08978a72e0)

Create new item > type name > select maven project > add git repository link > change branch to main > Build trigger > Go to add post built action > deploy ear/war to a container > Save and apply > Build now

![image](https://github.com/user-attachments/assets/2f11a6cf-93f9-4d49-9b90-13c1d2af38cf)

![image](https://github.com/user-attachments/assets/84b1d0c8-2317-43af-86a9-ad0977049701)

Open public ip of tomcat-server on web browser on port 8080

![image](https://github.com/user-attachments/assets/c1f03f76-292e-46c7-88f2-29625f1b26f3)

Go to manager app , add username: admin and password : admin

![image](https://github.com/user-attachments/assets/642a2846-3d6d-4224-81e9-7dab01ee1bd3)

Open /webapp

![image](https://github.com/user-attachments/assets/f27043ac-d544-454d-a888-4877bc51214f)

Your web application should open.

![image](https://github.com/user-attachments/assets/fe8789e0-de83-40de-bad1-899332665483)


### 3.Dockerization: 

The application is packaged into a Docker image and Image Storage: The Docker image is stored in Amazon ECR.

![image](https://github.com/user-attachments/assets/48ebed3c-11b4-45e6-8bce-ee0e9a704786)

Set password: passwd root
Generate ssh-key: ssh-keygen
Open /etc/ssh/sshd_config file and make the following changes:
PermitRoot login yes
Uncomment Pubkey authenticatiom yes
Password authentication yes
Permit empty yes
Esc > :wq! > enter
Run systemctl restart sshd, systemctl enable sshd

Configure aws iam user:

![image](https://github.com/user-attachments/assets/6beb1058-1deb-4501-a3dc-39a8617711b0)

Copy jenkins public ssh key in docker

![image](https://github.com/user-attachments/assets/00c4d0b6-eb8c-4f24-8025-111df98aea63)

Copy docker public ssh key in jenkins
Perform all the same steps in jenkins-server from set password. There will be one more step in jenkins server of connecting jenkins-server with jenkins. For that copy public ssh key of jenkins-server in jenkins-server itself.

Go to aws.com and create a repository in Elastic Container registry

![image](https://github.com/user-attachments/assets/fe9f28b8-6827-4f1a-9da0-0bc26f5ce4e6)

Go to jenkins > Manage jenkins > plugins > install **publish over ssh**

![image](https://github.com/user-attachments/assets/5d12f0f2-e955-459b-98cf-191e0cb450b6)

Manage jenkins > system > Go to publish over ssh tab and paste jenkins private key

![image](https://github.com/user-attachments/assets/c6081dff-5f35-4525-9811-e58613305f5d)

Add ssh-server and paste jenkins ip by running ip a s command in jenkins-server > test configuration. It should display Success.

![image](https://github.com/user-attachments/assets/e907e0d9-fe2f-4f48-9c0d-bfbe0f151854)

Add ssh-server and paste docker ip by running ip a s command in docker-server > test configuration. It should display Success.

![image](https://github.com/user-attachments/assets/eade17b8-56e9-4326-8b79-f2e910f3e384)

Apply > save
Go to your tomcat project in Jenkins > Configure > add post-built action > send artifacts over ssh:
The exec command is to synchronize files and directories from your local machine to the directory on the remote machine.

![image](https://github.com/user-attachments/assets/cab51c76-4e1d-4e64-8ab3-c102194b7e00)

In exec commands we have enter the commands to create a docker image of the built maven project and push the image in aws ecr.

![image](https://github.com/user-attachments/assets/f30b8aec-dee8-407e-9c6e-f7727a747235)

Apply > save > build Now
If build is successful image will be created and you can check it in your aws ecr repository.

![image](https://github.com/user-attachments/assets/b54979f1-ac01-4838-a54e-b6b34bcb05fc)

### 4.Deployment: 

The Docker image is deployed to a Kubernetes cluster.
Create IAM roles in aws and attach policy with instance :

![image](https://github.com/user-attachments/assets/cf99643f-d5d1-4736-8316-af4828c6f0b2)

Open cluster-server in terminal.
Set password: passwd root
Generate ssh-key: ssh-keygen
Open /etc/ssh/sshd_config file and make the following changes:
PermitRoot login yes
Uncomment Pubkey authenticatiom yes
Password authentication yes
Permit empty yes
Esc > :wq! > enter
Install eksctl and kubectl in cluster server

![image](https://github.com/user-attachments/assets/d6bf91d7-ca5b-4efd-bc66-2fa0b92c68a1)

Create cluster and nodegroup

![image](https://github.com/user-attachments/assets/34dd0a89-a183-47bd-8b4c-0b2e4b408438)

![image](https://github.com/user-attachments/assets/960a1d8c-6396-4e69-b64f-70d5655037ec)

Create one deployment.yml file and service.yml file

![image](https://github.com/user-attachments/assets/a8c3bbad-aef3-4e13-aad9-60c50042e4e5)

Paste the URI of the image in deployment.yml file.

![image](https://github.com/user-attachments/assets/e112cbe1-b81d-4085-bc36-7834fc340b24)

![image](https://github.com/user-attachments/assets/c847107a-511b-48e8-85f1-c0aa7682dbd5)

Add ssh-server and paste cluster ip by running ip a s command in docker-server > test configuration. It should display Success.

![image](https://github.com/user-attachments/assets/47d32efc-f429-4091-aeb2-2353afd19be7)

Apply > save
Go to your tomcat project in Jenkins > Configure > add post-built action > send artifacts over ssh:
These commands are to delete previous deployment and create new deploment and service.

![image](https://github.com/user-attachments/assets/e598e68a-3c9e-4342-bad0-fda69c2760df)

In the cluster server run the following command to display current services and vcopy the external ip and run http://external-ip:8080/webapp in web browser to run your java application.

![image](https://github.com/user-attachments/assets/7093182f-e205-416c-ad15-dc3390737510)

![image](https://github.com/user-attachments/assets/6b7f1f99-bf5b-4ae6-9aa8-3a0b2ec65edb)

In this way we have automated the whole process. If there are any modifications in the jsp file from github jenkins will automatically build the project and the changes will be reflected on the live webpage automatically.
If there are any errors in the modification the build will be failed and the webpage will not be updated. It will show the last successful built which will help in preventing our webpage from crashing.


































