# Kubernetes-practice
Kubernetes Installation Using KOPS on EC2
•	Create an EC2 instance or use your personal laptop.

 # minikube requirements #

* 2 cpu 
* t2.medium ubuntu
* mimikube installation process official kubernetes web site 
* docker
* 

# Dependencies required #

1) Python3
2) AWS CLI
3) kubectl


# PHYTHON 3 INSTALLATION #
$sudo apt update

$sudo apt install python3

Verify Python Installation:

$python3 –version  (to know the phython3 version)

Install pip (Python Package Manager)

$sudo apt install python3-pip

You can verify the installation of pip by running:

$pip3 –version

# Install AWS CLI #

Provide the below permissions to your IAM user. If you are using the admin user, the below permissions are available by default
1.	AmazonEC2FullAccess
2.	AmazonS3FullAccess
3.	IAMFullAccess
4.	AmazonVPCFullAccess

$sudo apt update

$sudo apt install -y python3-pip

$pip3 install awscli --upgrade –user

To check if the AWS CLI is installed correctly, run:

$aws –version


 Configure AWS CLI:
 
$aws configure

You will be prompted to enter the following information:
•	AWS Access Key ID
•	AWS Secret Access Key
•	Default region name (e.g., us-east-1)
•	Default output format (you can leave this as json

TO TEST THE AWS CLI:
To test that your AWS CLI configuration is working, you can use a simple command like to list your EC2 instances 

$aws ec2 describe-instances


# KUBECTL INSTALLATION #
* first install minikube  
* kubectl version –client
 (If it's not installed, you will see an error message. If it's already installed, you can skip the      installation steps.)
* sudo snap install kubectl --classic
* kubectl version --client (know the installtion process)


# INSTALL KOPS (Kubernetes operations) #
$ curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

$chmod +x kops-linux-amd64

$sudo mv kops-linux-amd64 /usr/local/bin/kops

Check the cops installed or not

$which kops


# Kubernetes Cluster Installation #
Please follow the steps carefully and read each command before executing.

Create S3 bucket for storing the KOPS objects.

$aws s3api create-bucket --bucket kops-mani-storage --region us-east-1 (review bucket name)


# Create the cluster #

$kops create cluster --name=demok8scluster.k8s.local --state=s3://kops-mani-storage --zones=us-east-1a --node-count=1 --node-size=t2.micro --master-size=t2.micro  --master-volume-size=8 --node-volume-size=8


# Important: Edit the configuration as there are multiple resources created which won't fall into the free tier. #
kops edit cluster myfirstcluster.k8s.local

 Build the cluster

$kops update cluster demok8scluster.k8s.local --yes --state=s3://kops-abhi-storage

This will take a few minutes to create............

After a few mins, run the below command to verify the cluster installation.

$kops validate cluster demok8scluster.k8s.local  




  
