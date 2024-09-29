Jenkins download commands
```yml
dnf install java-17-amazon-corretto -y
wget -O /etc/yum.repos.d/jenkins.repo \https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
dnf install jenkins -y
systemctl enable jenkins
systemctl start jenkins
```


Tomcat download commands
```yml
wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz
```

tomcat-users.xml
```yml
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
<user username="developer" password="developer" roles="manager-script"/>
<user username="tomcat" password="s3cret" roles="manager-gui"/>
```
eks-cluster-creation

# Install EKS Tool
```yml
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

Install Kubectl
```yml
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl 
kubectl version --client
```

Create EKS Cluster
```yml
eksctl create cluster --name my-cluster --region region-code --version 1.29 --vpc-public-subnets subnet-ExampleID1,subnet-ExampleID2 --without-nodegroup
```

