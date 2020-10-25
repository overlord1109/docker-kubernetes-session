# docker-kubernetes-session
Some notes / instructions and code to follow along with the Docker and Kuberenetes session for PICT students

# Prequisites:

[Docker](https://docs.docker.com/engine/install/) installed for your OS (available on Linux and Windows 10); check installation with

    $ docker -v

Do these [post-installation steps](https://docs.docker.com/engine/install/linux-postinstall/)

[minikube](https://minikube.sigs.k8s.io/docs/start/) installed for running a Kubernetes cluster locally; check installation with

    $ minikube start

[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed, check installation with

    $ kubectl version --client
    

# Docker:

## First container:

Let's pull an Ubuntu 16.04 image from the Docker registry:

    $ docker pull ubuntu:16.04

Check the image:
    
    $ docker images
    
Before running the image, let's verify our Host Ubuntu version in the terminal:
    
    $ cat /etc/lsb-release

Run our image:

    $ docker run -it ubuntu:16.04
    
Verify version in the interactive terminal:
    
    $ cat /etc/lsb-release
    
Let's create a file inside the container:

    $ touch myfile.txt
    $ ls

Start another container and see if the file is there:

    $ docker run -it ubuntu:16.04
    $ ls

### The Docker flow:

Run a docker image that exits after completing it's main process:

    $ docker run --rm -it ubuntu:16.04 sleep 5
    $ docker run --rm -it ubuntu:16.04 bash -c "sleep 3; echo all done"
    
Start a detached container:
    
    $ docker run -d -it ubuntu:16.04 bash

Check running containers:
    
    $ docker ps
    
Attach into the container:

    $ docker attach <container-name>


## Build and run our own image:

After cloning this repository, go to the directory with code for a simple node app with 'cd docker/node-app'. Build the image:

    $ docker build -t node-web-app:v1 .

Check your image:

    $ docker images

Run your image:

    $ docker run -p 48000:8080 -d node-web-app:v1
    
## Docker registry:

First, create an account at https://hub.docker.com/ then login via the command line:

    $ docker login
    $ docker tag node-web-app:v1 overlord1109/node-app:v1
    $ docker push overlord1109/node-app:v1
    
# Kubernetes:

## Start a local Kubernetes cluster:

We are going to use minikube to deploy a local Kubernetes cluster, and see what all functionalities it provides.

    $ minikube start --memory=2g --driver=docker --cpus=2
    $ minikube dashboard

Let's check what namespaces we have by default

    $ kubectl get namespace
    
## Pods:

Before you create your first pod:

    $ eval $(minikube docker-env)
    $ docker build -t node-web-app:v1 .

You can go ahead and create your first pod, like this:

    $ kubectl run hello-app --image=node-web-app:v1 --image-pull-policy=Never

## Services:

We will now expose our pod via service, like this:

    $ kubectl expose pod hello-app --type=LoadBalancer --port=8080
    $ kubectl get service
    $ minikube ip
    
## Deployments:

Let’s create our deployment:

Change directory to kubernetes folder, where you’ll find a deployment.yaml

    $ kubectl apply -f deployment.yaml
    $ kubectl get deployments

Small experiment, what happens if I delete a pod:

    $ kubectl delete pod <pod-name>


