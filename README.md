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
