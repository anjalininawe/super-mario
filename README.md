# $$\color{green}{\textbf Project: 🎮 \color{red} \textbf {Super} \ \color{orange} \ \textbf Mario  \ \textbf Bros 🍄🐢}$$

##  $\color{blue} \textbf {Project  Workflow}$
Step 1 → Login and basics setup

Step 2 → Setup Docker ,Terraform ,aws cli , and Kubectl

Step 3 → IAM Role for EC2

Step 4 →Attach IAM role with your EC2

Step 5 → Building Infrastructure Using terraform

Step 6 → Creation of deployment and service for EKS



### $\color{red} \textbf {Step 1 → Login  and  basics  setup}$
1. Click on launch Instance
   <img width="1901" height="521" alt="image" src="https://github.com/user-attachments/assets/a3801fea-048e-4439-8a55-20ac8fe03057" />

2. Connect to EC2-Instance
   <img width="1919" height="460" alt="image" src="https://github.com/user-attachments/assets/306873d2-3289-4ca4-924a-4c92fdde3047" />


   
5. Attach role to ec2 instance

### $\color{red} \textbf {Step 2 → Setup  Tools}$

````
sudo apt update -y
````
$\color{blue} \textbf {Setup  Docker:}$
````
sudo apt install docker.io -y
sudo systemctl start docker
sudo usermod -aG docker ubuntu
newgrp docker
docker --version
````
````
sudo yum install docker -y
sudo systemctl start docker
sudo usermod -aG docker ec2-user
newgrp docker
docker --version
````

$\color{blue} \textbf {Setup Terraform:Ubuntu}$
````
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

````
- Amazon linux
````
sudo yum install -y yum-utils shadow-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum install terraform -y
````
${\color{blue} \textbf {Setup  AWS CLI:}}$
````
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip 
unzip awscliv2.zip
sudo ./aws/install
aws --version

````

## ${\color{blue} \textbf {Install kubectl}}$
Download the latest release with the command:
````
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
````

Install kubectl:
````
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
````
Note:
If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:
````
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
````
````
kubectl version --client
````
### $\color{red} \textbf {Step 3 → IAM  Role  for  EC2}$
create role:
<img width="1878" height="784" alt="image" src="https://github.com/user-attachments/assets/869bf36e-c3ca-466b-b8b0-640b941759bd" />


### $\color{red} \textbf {Step 4 →Attach  IAM  role  with your  EC2 }$
go to EC2 
click on actions → security → modify IAM role option
- administrator access
- eks
- <img width="1503" height="754" alt="image" src="https://github.com/user-attachments/assets/fa8da0cb-d9e9-4036-b928-1f7e19ad483f" />


<img width="1861" height="459" alt="image" src="https://github.com/user-attachments/assets/6a16f2b4-1b4c-4ee5-b2b5-75465b42cd68" />


<img width="1875" height="586" alt="image" src="https://github.com/user-attachments/assets/c37d9f8b-be60-4254-9468-9856d384f26a" />


### $\color{red} \textbf {Step 5 → Building Infrastructure  Using  terraform}$
$\color{blue} \textbf {Install  GIT}$
````
git clone https://github.com/anjalininawe/super-mario.git
````
````
cd Project-Super-Mario
cd EKS-TF
````
````
vim backend.tf
````
<img width="1104" height="228" alt="image" src="https://github.com/user-attachments/assets/e20f9cfa-ce07-4fdc-b3d7-7841ac6f6bac" />


$\color{blue} \textbf {Create \ Infra:}$
````
terraform init
terraform plan
terraform apply --auto-approve
````

````
aws eks update-kubeconfig --name EKS_CLOUD --region eu-north-1 --profile eks
````

### $\color{red} \textbf {Step 6 → Creation  of  deployment  and service  for  EKS}$
change the directory where deployment and service files are stored use the command →
````
cd ..
````
$\color{blue} \textbf {create  the  deployment}$
````
kubectl apply -f deployment.yaml
````
$\color{blue} \textbf {Now create  the service}$
````
kubectl apply -f service.yaml
kubectl get all
kubectl get svc mario-service
````
copy the load balancer ingress and paste it on browser and your game is running
<img width="1755" height="84" alt="image" src="https://github.com/user-attachments/assets/99f508eb-26f1-43c2-836e-c0a465a0e29a" />





$\color{green} \textbf {Final Output: Enjoy The Game 🎮}$

<img width="1919" height="902" alt="image" src="https://github.com/user-attachments/assets/abfdb050-67c5-4d48-a293-86be48463168" />


**Delete Infra**
````
 terraform destroy -auto-approve
````
