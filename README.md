# Udagram Microservices
 Udacity Cloud Developer Nanodegree

## Getting Started
Udagram is a simple cloud application developed which allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

### Prerequisites
You need to install:  
[Docker](https://docs.docker.com/docker-for-windows/install/)  
[AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-linux.html)  
[Eksctl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)  
[AWS-iam-authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)  
[Kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)  

### Installation
Test that your installation was Successful with the following commands:  
`docker --version`  
`aws --version`  
`eksctl version`  
`kubectl version --short --client`  
`aws-iam-authenticator version`  


### Setup Environment Variables

Set up your own values:
```
export POSTGRESS_USERNAME=your postgress username;
export POSTGRESS_PASSWORD=your postgress password;
export POSTGRESS_DB=your postgress database;
export POSTGRESS_HOST=your postgress host;
export AWS_REGION=your aws region;
export AWS_PROFILE=your aws profile;
export AWS_BUCKET=your aws bucket name;
export JWT_SECRET=your jwt secret;
```

### Setup Docker Enviroment
Build the images: 
`docker-compose -f docker-compose-build.yaml build --parallel`  

List your docker images to check if they have been built:
`docker images`  

Run your docker containers: 
`docker-compose up`   

To exit run `control + C`


Push your docker images:
 `docker-compose -f docker-compose-build.yaml push`  


Check your Docker Hub.


### Create a Kubernetes Cluster on Amazon EKS with eksctl

use AWS CLI or AWS console 


 ### Create Kubernetes Components (Configmaps and Secrets)

- `cd udacity-c3-deployment/k8s`

- `kubectl apply -f .`


### Check your Pods Status

`kubectl get all`  


### CI/CD with TravisCL
- Sign up for [TravisCL](https://travis-ci.com) and connect your Github application repository to TrivisCL.
- Add `.travis.yml` file to the root of the application.
- Copy and paste the following code into your `.travis.yml` file:
```
language: minimal

services: docker

env:
  - DOCKER_COMPOSE_VERSION=1.23.2

before_install:
  - docker -v && docker-compose -v
  - sudo rm /usr/local/bin/docker-compose
  - curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-`uname -s`-`uname -m` > docker-compose
  - chmod +x docker-compose
  - sudo mv docker-compose /usr/local/bin
  - curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
  - chmod +x ./kubectl
  - sudo mv ./kubectl /usr/local/bin/kubectl

install:
  - docker-compose -f udacity-c3-deployment/docker/docker-compose-build.yaml build --parallel 
```  
- Add your environment variables to the project repository in [TravisCL](https://travis-ci.com) by selecting the setting option.

- Commit and Push your changes to trigger a Travis CI build.
> Travis only runs builds on the commits you push after you’ve added a `.travis.yml` file.