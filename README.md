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

**Step-1:**<br>
➢ Setup CI/CD with GitHub, Jenkins, Maven & Tomcat.<br>
➢ Setup Jenkins<br>
➢ Setup & Configure Maven, Git.<br>
➢ Setup Tomcat Server.<br>
➢ Integrating GitHub, Maven, Tomcat Server with Jenkins.<br>
➢ Create a CI and CD Job.<br>
➢ Test the Deployment<br>

**Step-2:**<br>
➢ Setup CI/CD with GitHub, Jenkins, Maven & Docker.<br>
➢ Setting up the docker Environment.<br>
➢ Create an Image and Container on Docker Host.<br>
➢ Integrate Docker Host with Jenkins.<br>
➢ Create CI/CD Job on Jenkins to build and deploy on container.<br>

**Step-3:**<br>
➢ Build and Deploy on Container.
➢ CI/CD with GitHub, Jenkins, Maven & Kubernetes.<br>
➢ Setting up the Kubernetes (EKS).<br>
➢ Write pod service and deployment manifest file.<br>
➢ CI/CD Job to build code on Jenkins & Deploy it on Kubernetes.<br>

**Step-4:**<br>
➢ Deploy artifacts on the Kubernetes<br>
➢ Write codes in the artifacts of docker and Kubernetes which we want to run.<br>
➢ Now build the code in Jenkins.<br>
➢ Check in Kubernetes the pods are getting created or not.<br>
➢ Now copy the service IP and paste it in the browser and check the output.<br><br>


**Solution**<br>
   
i. We will create three EC2 instances (**Git_Inst, Jenkins, and Tomcat**) on AWS, using **Amazon Linux** as the server. The **Git and Tomcat instances** will have an **instance type of t2.micro**, while the **Jenkins server** will use **t2.medium**. <br> 

![image](https://github.com/user-attachments/assets/f14348df-4934-4ba8-afe2-cdd2cd093684)<br><br>

ii. We have made a new security group and gave access to the ports below.<br>

![image](https://github.com/user-attachments/assets/e5ba9bec-8153-4d30-a6f2-088467306fdc)<br><br>

iii. We will now connect to the terminal of Git instance, set the hostname to GitInstance and install git.<br>

![image](https://github.com/user-attachments/assets/8ea8c119-3bd1-43fb-a149-ddf03e447cdf)<br><br>


iv. We will now establish SSH connection using ssh-keygen. We use ssh-keygen in DevOps to generate secure SSH keys for authenticating and encrypting connections to remote servers.<br>

![image](https://github.com/user-attachments/assets/aad1ebb7-b7ce-4763-9ff5-0050ccb21b27)<br><br>


v. After getting the public key we will paste it in the git repository under settings >> SSH and GPG keys >> Add new SSH Key<br>

![image](https://github.com/user-attachments/assets/af0dd08f-6518-4daf-b226-07dfd5156c84)<br><br>

vi. In the Git_Inst terminal, we will first initialize Git. Once initialized, we will successfully push the files to the Git repository <br>

![image](https://github.com/user-attachments/assets/95320354-f49a-47e8-a94b-78b74b81a515)<br><br>

![image](https://github.com/user-attachments/assets/99e81b15-6077-448d-9911-ece85a9674e8)<br><br>

vii. We will now connect to Jenkins terminal, set the hostname,install java, install jenkins and then start and enable Jenkins .<br>

```sh
wget -O /etc/yum.repos.d/jenkins.repo \ https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
dnf install jenkins -y
systemctl enable jenkins
systemctl start jenkins
```

![image](https://github.com/user-attachments/assets/e9c47c17-c016-494a-a0a8-b6be1cca31bb)<br><br>
![image](https://github.com/user-attachments/assets/861fb6c8-56f0-40d4-ac34-fb9c3473d6ec)<br><br>
![image](https://github.com/user-attachments/assets/1d41d09c-b892-4a72-8ede-9cbc689e9fc4)<br><br>

viii. We will now paste the public IP on the browser along with port 8080 to unlock Jenkins and then copy the command highlighted in pink and paste it on the terminal to get the administrator password.<br>

![image](https://github.com/user-attachments/assets/f2684bfb-5574-4647-9b0f-e2f1e28d114e)<br><br>
![image](https://github.com/user-attachments/assets/23a5551d-d766-4036-b4cf-e275c5253cf5)<br><br>

ix. After pasting the administrator password,  we will be redirected to the page as shown in the sc reenshot below and there we will click on Install suggested by plugins to install Jenkins.After the installation, set up the username and password to log in to Jenkins, then click on 'Save and Finish'.<br>

![image](https://github.com/user-attachments/assets/273a05b7-e890-4d1e-8320-4df0523a721e)<br><br>
![image](https://github.com/user-attachments/assets/b377b12c-3483-4e07-bd54-1ad30309080c)<br><br>
![image](https://github.com/user-attachments/assets/daad0810-cb8b-4b12-b6b9-7bf20a898c1f)<br><br>
![image](https://github.com/user-attachments/assets/5374157f-da69-4b75-a288-b1b03457c369)<br><br>


x. We will then be redirected to Jenkins page where we are supposed to go on Dashboard and click on configure to generate an API token. Here we will simply click on create token and then copy it.<br>

![image](https://github.com/user-attachments/assets/fe1fbc66-eac7-48a5-a047-092531364bf8)<br><br>

xi. Go to GitHub settings, navigate to Webhooks, and add a new webhook. In the Payload URL section, paste your Jenkins URL up to port 8080 and add /github-webhook/. Select application/json as the content type, and paste the token generated in Jenkins into the Secret section<br>

![image](https://github.com/user-attachments/assets/fc4e8c64-ed34-4d81-b5dd-d17ab0754fe4)<br><br>

xii. We will then install mavens in the Jenkins terminal.<br>

![image](https://github.com/user-attachments/assets/2df65ec5-ad34-4a1b-aa85-f6ba5ff32192)<br><br>

xiii. Go to the Jenkins URL, navigate to the dashboard, then Manage Jenkins > Plugins > Available Plugins, search for and install Maven Integration. Next, go to Installed Plugins, search for Git Branch, disable it, and GitHub login will be enabled automatically.We will then click on restart once no jobs are running and post that Jenkins will restart<br>

![image](https://github.com/user-attachments/assets/ea0b3273-c384-4e47-9367-0c4dc6b97620)<br><br>
![image](https://github.com/user-attachments/assets/a0b26e5e-1bfe-4021-a7ce-6dff3bd9bcb2)<br><br>

xiv.Install Git on the Jenkins server. Later, run mvn -v to find the Maven version and paths for Maven and Java, which will need to be added in the Tools section<br>

![image](https://github.com/user-attachments/assets/d7ed9ff8-1ded-4319-80a1-5a5ba6eee985)<br><br>
![image](https://github.com/user-attachments/assets/5519392c-4bc8-4521-b1f0-09704624bcc3)<br><br>
![image](https://github.com/user-attachments/assets/9d5cf290-0631-4154-b4bb-70311e7f383d)<br><br>
![image](https://github.com/user-attachments/assets/056cf749-1f77-4c3f-8f58-eefa50cfaa46)<br><br>

xv. After this we will go to dashboard and click on new item and then select maven project and click on OK.<br>

![image](https://github.com/user-attachments/assets/cb3c9a9e-fffe-4a67-88d0-7576cc8c1832)<br><br>

xvi. Here we selected Git and added the repository URL which we will find on GitHub under code in https. We We will also change the branch to main from master and click on build now.<br>

![image](https://github.com/user-attachments/assets/e37a813e-bc2e-495a-8cb8-258c7a8be542)<br><br>
![image](https://github.com/user-attachments/assets/79f065b7-2c0a-41fa-92d6-68636a210c28)<br><br>
![image](https://github.com/user-attachments/assets/97a47a26-05d3-4c3e-b853-49e4b85a9578)<br><br>

xvii. We will then connect to Tomcat terminal and install Java.<br>

![image](https://github.com/user-attachments/assets/c393f206-5ed3-4360-bc00-4fee171ea721)<br><br>

xviii. We will then go to apache tomcat link and select the tar.gz file of version 9 and then copy the link.<br>

![image](https://github.com/user-attachments/assets/d4fc1a9f-57f6-4135-8733-bc5e0b61822a)<br><br>

xix. Navigate to the /opt directory using cd /opt, then download the tar.gz file with wget followed by the URL. Once downloaded, extract it using tar -xzvf yourfile.tar.gz. This will allow you to make the necessary installations and changes.We will then use ls command to check if the file is installed.We will go to the apache-tomcat directory and then go to the bin directory for
startup and shutdown of the system<br>

![image](https://github.com/user-attachments/assets/bea81c4a-cf37-447d-824c-7eeb9b9e8445)<br><br>
![image](https://github.com/user-attachments/assets/3721c066-5663-4ee8-bdef-a8d698fa2fe0)<br><br>
![image](https://github.com/user-attachments/assets/84ec1264-5fed-4335-b2a6-ea9814daefe8)<br><br>


xx. We will now paste the public ip of tomcat along with port 8080 on the browser.<br>

![image](https://github.com/user-attachments/assets/c98f4b3f-bcf1-413c-8148-39269bf13573) <br><br>


xxi. We then go to tomcat Apache file and find the context.xml file and select the last two files (host-manager and manager)and then comment out the valve in the vim file.<br>

![image](https://github.com/user-attachments/assets/91e5cafc-c6df-40f4-832a-4aa08e612950)<br><br>
![image](https://github.com/user-attachments/assets/deae313e-6545-4c03-b11e-ed533899992a)<br><br>

xxii. We will go to conf directory to edit the tomcat-users.xml file to set the credentials.

![image](https://github.com/user-attachments/assets/19f09ea9-4944-4afc-be87-242bb6bfa85b)<br><br>
![image](https://github.com/user-attachments/assets/7c2069e8-02a6-4209-9203-0ca9d9dbabc7)<br><br>

Refer to the code below

```sh
tomcat-users.xml
  <role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-status"/>
  <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
  <user username="developer" password="developer" roles="manager-script"/>
  <user username="tomcat" password="s3cret" roles="manager-gui"/>
```

xxiii. After making changes to the vim file we will again shutdown and startup the system to reflect the changes.<br>

![image](https://github.com/user-attachments/assets/71c1fe27-438d-4ec5-bf69-202c2d48e16e)<br><br>


xxiv. We will now refresh the browser and we will get a page asking to add credentials
for username and password.

![image](https://github.com/user-attachments/assets/ee1adde1-e9f2-4ac3-8035-05abffad4ee9)<br><br>

xxv. We will now go to Jenkins browser >> manage Jenkins >> Add credentials<br>

![image](https://github.com/user-attachments/assets/00512de0-f5b0-47e0-b395-7ee1f6d0cc44)<br><br>

xxvi. The credentials should be same as that added in the vim file i.e in the tomcat-users.xml where we have set the password and the username<br>

![image](https://github.com/user-attachments/assets/3f76b25f-a71c-4fe5-a8d5-a37594c24f5b)<br><br>

xxvii. We will then create a new item and select mavens and then build the project.<br>

![image](https://github.com/user-attachments/assets/db76ebe4-6cbc-448c-a07e-2ba9228b170a)<br><br>

xxviii. We will also install deploy to container in the plugins.<br>

![image](https://github.com/user-attachments/assets/3b89f2d5-c258-45f7-a9c7-a5056fdd64e6)<br><br>

xxix. We have added the credentials successfully.<br>

![image](https://github.com/user-attachments/assets/a03e0729-c638-4029-a155-88466b7f6fd2)<br><br>

xxx. We will select the installed tomcat version and build.

![image](https://github.com/user-attachments/assets/62df4346-1ae6-4c45-b42c-49021490d0bc)<br><br>
![image](https://github.com/user-attachments/assets/d83aa911-9274-43d9-a5f7-3265ade32f9a)<br><br>


xxxi. We will now connect to Docker terminal.<br>

![image](https://github.com/user-attachments/assets/bcb8c3f5-09fa-492e-8922-cd5fbbd8b6b4)<br><br>

xxxii. In order to establish connection between Jenkins and Docker we will interchange the keys. We will paste the Jenkins key in the docker terminal under vim authorized_keys and as for Jenkins we will paste docker and Jenkins both keys in the terminal under
vim authorized_keys<br>

![image](https://github.com/user-attachments/assets/bca1bccb-d3f8-4d06-a823-d24d13db1852)<br><br>

xxxiii. We will then configure AWS.<br>

![image](https://github.com/user-attachments/assets/dbe7fb82-e42f-4272-9b70-1bdadd4d4083)<br><br>

xxxiv. We will restart and enable sshd.<br>
![image](https://github.com/user-attachments/assets/72a2be31-2ded-4c3f-89ff-0a5106d515bb)<br><br>

xxxv. We will install Publish over SSH.<br>

![image](https://github.com/user-attachments/assets/87420afa-4632-452b-83d2-8d47abf83337)<br><br>

xxxvi. We will navigate to manage Jenkins >> system<br>

![image](https://github.com/user-attachments/assets/efc7e8fc-04d8-479b-8e3a-cf65a3d9d3c6)<br><br>

xxxvii. We will use cat command to get private key of Jenkins which needs to be pasted inside publish over
ssh.<br>

![image](https://github.com/user-attachments/assets/d4868e16-c4a1-4b2a-bb8b-e1cc40149c5c)<br><br>
![image](https://github.com/user-attachments/assets/fd28cf4a-fc85-4b80-a027-323a64532907)<br><br>


xxxviii. We will paste IP address of Jenkins under hostname<br>

![image](https://github.com/user-attachments/assets/3a67ffd6-a9fa-44bb-96ae-fb4ea429f2e7)<br><br>
![image](https://github.com/user-attachments/assets/c9a090f9-c0cc-4e23-8dee-e17b75ccda1c)<br><br>


xxxix. We will then start Docker<br>

![image](https://github.com/user-attachments/assets/ef4d36e5-79be-4671-961b-2673c1ac4c85)<br><br>
![image](https://github.com/user-attachments/assets/dda671fd-b855-40d4-bc01-4e9fc4654302)<br><br>

xxxx. We will go to Jenkins and give the permit root login access under the sshd_config file.<br>

![image](https://github.com/user-attachments/assets/e95f7455-2f72-4685-8111-27171125af21)<br><br>
![image](https://github.com/user-attachments/assets/6c4116ba-ace8-48fa-b4ac-c2337719a1ad)<br><br>

xxxxi. We have added SSH server for docker as well<br>

![image](https://github.com/user-attachments/assets/7b42a664-bc7d-4fc9-aedb-6bf0211e9c64)<br><br>

xxxxii. Here we will select Send build artifacts over SSH<br>

![image](https://github.com/user-attachments/assets/3213cf34-d3d8-40ef-a226-7487b99bc65b)<br><br>

xxxxiii. We will now configure Jenkins where we have used rsync -avh command with ip of docker. We will paste the path which
we will get from console output of the job.<br>

![image](https://github.com/user-attachments/assets/bc7ae35c-248f-4565-b252-23cb82bf8cca)<br><br>
![image](https://github.com/user-attachments/assets/006610da-ee46-4259-b91b-9ebccd28ec36)<br><br>


xxxxiv. We will then create an ECR Repo and click View push commands<br>

![image](https://github.com/user-attachments/assets/890668cb-a088-4587-aedd-05d095ee757d)<br><br>
![image](https://github.com/user-attachments/assets/e8bfad3d-6c47-48e3-9873-3d31f7ab7641)<br><br>

xxxxv. We will copy these four commands to paste it while configuring docker in Exec command<br>

![image](https://github.com/user-attachments/assets/74213153-1826-433a-8f53-3272c395c362)<br><br>
![image](https://github.com/user-attachments/assets/ac86d382-3785-42da-9d2c-17b9e5c5a2fe)<br><br>
![image](https://github.com/user-attachments/assets/343016fa-f676-4402-ba04-b6ed3cd660bc)<br><br>
![image](https://github.com/user-attachments/assets/e59f0130-2680-4143-bf57-cb50d645c073)<br><br>

xxxxvi. We will create a new instance for cluster, with ubuntu server and instance type t2.micro and attach the role to the Kubernetes instance with the access to permissions of eks, elasticcontairregistry and iam full access.<br>

![image](https://github.com/user-attachments/assets/562a3769-21bb-4247-892e-a837fdc949d6)<br><br>
![image](https://github.com/user-attachments/assets/7f563b4a-54e6-4f1a-94a1-62b43928c27e)<br><br>
![image](https://github.com/user-attachments/assets/796fc366-ff2e-4199-a5dc-66cd4881a79a)<br><br>

xxxxvii. We will now connect to the terminal of EKS cluster<br>
![image](https://github.com/user-attachments/assets/fc681b22-570c-4ef1-8545-44abe4a6d624)<br><br>

xxxxviii. Here we have set the hostname and then we unzipped the file.<br>

![image](https://github.com/user-attachments/assets/a68591cd-ba3c-4e43-8e72-1532c41862df)<br><br>


xxxxix. We will install awscli since we are using ubuntu server.<br>

![image](https://github.com/user-attachments/assets/eac708c3-4658-4ab6-a3b7-abecdcd33fb0)<br><br>
![image](https://github.com/user-attachments/assets/9f9b28f7-f797-4eea-8190-f639cf89ee84)<br><br>

xxxxx. We will establish SSH connectio between Jenkins, docker and cluster by interchanging the keys in vim file as we have done to establish connection between Docker and Jenkins<br>

xxxxxi. We will install tools like EKS, Kubectl.<br>

![image](https://github.com/user-attachments/assets/5bc1342e-12df-471d-80e0-a832ae258296)<br><br>
![image](https://github.com/user-attachments/assets/250bb204-bda5-4148-8b49-66a8eb578793)<br><br>

xxxxxii. Install kubectl and create a cluster with region code and subnets<br>

![image](https://github.com/user-attachments/assets/176b0343-31d9-40cb-9887-fee357807346)<br><br>
![image](https://github.com/user-attachments/assets/4b2cca23-73ee-4fcf-a2ae-baa43b2f0493)<br><br>

```sh
eksctl create cluster --name my-cluster --region region-code --version 1.29 --vpc-public-subnets subnet-ExampleID1,subnet-ExampleID2 --without-nodegroup
```

xxxxxiii. We will create a node group.<br>

![image](https://github.com/user-attachments/assets/7beb08ff-7f19-4b3b-90c2-33ac25d0c3cf)<br><br>

```sh
create node group
     eksctl create nodegroup \
  --cluster my-cluster \
  --region us-east-2 \
  --name my-node-group \
  --node-ami-family Ubuntu2004 \
  --node-type t2.small \
  --subnet-ids subnet-086ced1a84c94a342,subnet-01695faa5e0e61d97 \
  --nodes 3 \
  --nodes-min 2 \
  --nodes-max 4 \
  --ssh-access \
  --ssh-public-key /root/.ssh/id_rsa.pub
```

xxxxxiv. We will then permit root login access under vim /etc/ssh/sshd_config and post that restart the system again to reflect the changes<br>

![image](https://github.com/user-attachments/assets/ef704045-6c00-4ef0-b1e8-e8cc3bcb864e)<br><br>
![image](https://github.com/user-attachments/assets/4aa325a1-3888-4125-a55c-d4366b8e34ea)<br><br>

xxxxxv. We will create vim deployment.yml and service.yml file. We will paste the URL of ECR image in the image section in deployment.yml file.<br>

![image](https://github.com/user-attachments/assets/239568ec-f74e-4ce1-84e3-dd652c586d9f)<br><br>
![image](https://github.com/user-attachments/assets/e322fe5b-2b8f-4248-95d3-a27b84c1da9b)<br><br>

Deployment.yml
```sh
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-project-deployment
  labels:
    app: regapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: regapp
  template:
    metadata:
      labels:
        app: regapp
    spec:
      containers:
      - name: regapp
        image: copy latest image from ecr here
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
```

Service.yml
```sh
apiVersion: v1
kind: Service
metadata:
  name: my-service
  labels:
    app: webapp
spec:
  selector:
    app: webapp
  ports:
    - port: 8080
      targetPort: 8080
  type: LoadBalancer
```

xxxxxvi. In Jenkins dashboard we will add SSH server for cluster.<br>
![image](https://github.com/user-attachments/assets/2cd5110d-af9f-4f0f-9816-0be6627d4c61)<br><br>

xxxxxvii. We will add the below kubectl commands in Exec command for cluster.<br><br>

```sh
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

xxxxxvii. Once we will deploy it using the above commands and next time we will use rollout command to deploy<br>
![image](https://github.com/user-attachments/assets/fe220562-639f-4cb7-bad9-2ffda7a7cae8)<br><br>

```sh
kubectl rollout restart deployment/mahek-deployment
```

xxxxxviii.We will now Build the job.<br>

![image](https://github.com/user-attachments/assets/c872d804-4784-45b8-b992-0b4be0cccd45)<br><br>

xxxxxix.We will use kubectl get svc command to get the IP in the cluster terminal.<br>

![image](https://github.com/user-attachments/assets/115d1b31-28a5-4fc1-8337-a6ab2e87f338)<br><br>

xxxxxx. We will create a docker file inside github repository.<br>

![image](https://github.com/user-attachments/assets/a543d623-5ec6-42e3-be7b-bc94597cd24e)<br><br>

xxxxxxi. We will go to Github repository and add a new file that is index php file inorder to create website.<br>

![image](https://github.com/user-attachments/assets/4cf6bb95-7d94-4354-b0a7-42e6cfb82438)<br><br>

xxxxxxii.We will paste the IP which we got through the kubectl svc command and add:8080/webapp/ after the IP for accessing the website.<br>

**Final output is here**<br>

![image](https://github.com/user-attachments/assets/b8086f89-59e3-4cba-9b05-8d468585d39d)



























































































































