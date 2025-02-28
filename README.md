# 🚀 CI/CD Pipeline for Java Web App using AWS, Jenkins, Docker & Kubernetes

## 📌 Problem Statement  

Create an end-to-end CI/CD pipeline in AWS platform using Jenkins as the
orchestration tool, Github as the SCM, Maven as the Build tool, deploy in a
docker instance and create a Docker image, Store the docker image in ECR,
Achieve Kubernetes deployment using the ECR image. Build a sample java
web app using maven.<br><br>

### Requirements  

✔️ **CI/CD pipeline System** <br>  
✔️ **Git** - Local version control system. <br>  
✔️ **GitHub** - Distributed version control system. <br>  
✔️ **Jenkins** - Continuous Integration tool. <br>  
✔️ **Maven** - Build tool. <br>  
✔️ **Docker** - Containerization. <br>  
✔️ **Kubernetes** - Container management tool. <br><br> 


Steps<br>
   
i. We will create three EC2 instances (**Git_Inst, Jenkins, and Tomcat**) on AWS, using **Amazon Linux** as the server. The **Git and Tomcat instances** will have an **instance type of t2.micro**, while the **Jenkins server** will use **t2.medium**. <br> 

![image](https://github.com/user-attachments/assets/f14348df-4934-4ba8-afe2-cdd2cd093684)<br><br>

ii. We have made a new security group and gave access to the ports below.<br>

![image](https://github.com/user-attachments/assets/e5ba9bec-8153-4d30-a6f2-088467306fdc)<br><br>

iii. We will now connect to the terminal of Git instance, set the hostname to GitInstance and install git.<br>

![image](https://github.com/user-attachments/assets/8ea8c119-3bd1-43fb-a149-ddf03e447cdf)<br><br>

```sh
hostnamectl set-hostname developer
bash
yum install git -y
```

iv. We will now establish SSH connection using ssh-keygen. We use ssh-keygen in DevOps to generate secure SSH keys for authenticating and encrypting connections to remote servers.<br>

![image](https://github.com/user-attachments/assets/aad1ebb7-b7ce-4763-9ff5-0050ccb21b27)<br><br>

```sh
ssh-keygen 
cd .ssh/
cat id_rsa.pub (to check the key id )
```

v. After getting the public key we will paste it in the git repository under settings >> SSH and GPG keys >> Add new SSH Key 

![image](https://github.com/user-attachments/assets/af0dd08f-6518-4daf-b226-07dfd5156c84)













