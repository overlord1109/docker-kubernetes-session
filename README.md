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

After cloning this repository, go to the directory with code for a simple node app with 'cd docker/node-app'. Build the image:

    $ docker build -t node-web-app:v1 .

Check your image:

    $ docker images

Run your image:

    $ docker run -p 48000:8080 -d node-web-app:v1
