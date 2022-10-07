# Setup Kubernetes on Amazon EKS

4.2 Setup maven

For setting up the maven Goto -> Manage Jenkins -> Global Tool Configuration -> maven

5. Update visudo and assign administration privileges to jenkins user

vi /etc/sudoers
jenkins ALL=(ALL) NOPASSWD: ALL
sudo su - jenkins

6. Install Docker

yum install docker -y
docker --version
service docker start
service docker status
usermod -aG docker jenkins


7.1 Configure AWS CLI

aws configure

AWS Access Key ID [None]:
AWS Secret Access Key [None]:
Default region name [None]:
Default output format [None]:
You can find this information by going into AWS -> My Security Credentials

You can click on the Create New Access Key and it will let you generate - AWS Access Key ID, AWS Secret Access Key.






You can follow same procedure in the official  AWS document [Getting started with Amazon EKS – eksctl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)   

#### Pre-requisites: 
  - an EC2 Instance 

#### AWS EKS Setup 
1. Setup kubectl   
   a. Download kubectl version 1.20  
   b. Grant execution permissions to kubectl executable   
   c. Move kubectl onto /usr/local/bin   
   d. Test that your kubectl installation was successful    
   ```sh 
   curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
   chmod +x ./kubectl
   mv ./kubectl /usr/local/bin 
   kubectl version --short --client
   ```
2. Setup eksctl   
   a. Download and extract the latest release   
   b. Move the extracted binary to /usr/local/bin   
   c. Test that your eksclt installation was successful   
   ```sh
   curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
   sudo mv /tmp/eksctl /usr/local/bin
   eksctl version
   ```

Create eks cluster using eksctl

In all the previous 9 steps we were preparing our AWS environment. Now in this step, we are going to create EKS cluster using eksctl

You need the following in order to run the eksctl command

Name of the cluster : --name jhooq-test-cluster
Version of Kubernetes : --version 1.17
Region : --name eu-central-1
Nodegroup name/worker nodes : worker-nodes
Node Type : t2.micro
Number of nodes: -nodes 2

Here is the eksctl command -

eksctl create cluster --name naresh-test-cluster --version 1.20 --region ap-south-1 --nodegroup-name worker-nodes --node-type t2.micro --nodes 2
