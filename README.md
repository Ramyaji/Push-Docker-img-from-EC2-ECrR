# Push-Docker-img-from-EC2-ECR

How to push docker image from EC2 to ECR
1.clone repository which have docker file in it
2.create the docker image from docker file
3. push docker image to ECR


1.Create EC2 Instance

*connect to gitbash (open gitbash from directory with .pem file in it)
$ssh -i "PK.pem" ubuntu@ec2-13-126-234-119.ap-south-1.compute.amazonaws.com
$sudo -i (to become root)
$apt-get update

2.install docker in ubuntu (search for coomands in google)
$sudo apt install apt-transport-https ca-certificates curl software-properties-common
$curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
$apt-cache policy docker-ce
$sudo apt install docker-ce
$sudo systemctl status docker

3.Clone repository (git clone repo url ssh or https) with dockerfile in it
$git clone https://github.com/waldemarnt/node-docker-example.git
$cd node-docker-example/
$ls
node-docker-example  snap

4.Create docker image from docker file
$docker build -t ramyanodedockerimage:tag .
$docker images

5.Install AWS CLI
$apt  install awscli
$apt install python3-pip
$aws configure
Acess key
secret key
region



5.Create ECR elastic container registry in aws
copy commands from console to push image into ECR
*Retrieve an authentication token and authenticate your Docker client to your registry.
$aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 974828623032.dkr.ecr.ap-south-1.amazonaws.com

*After the build completes, tag your image so you can push the image to this repository:
$docker tag ramyanodedockerimage:tag 974828623032.dkr.ecr.ap-south-1.amazonaws.com/pawan_nodejs:latest $docker push 974828623032.dkr.ecr.ap-south-1.amazonaws.com/pawan_nodejs:latest

*Run the following command to push this image to your newly created AWS repository:
$docker push 974828623032.dkr.ecr.ap-south-1.amazonaws.com/pawan_nodejs:latest

check the ECR you will get the docker image get pushed successfully
