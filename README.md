# Guess the name
Guess the name of a child or pet to be named.

## Prerequisites

### Install
Git - Ubuntu: sudo apt install git
DockerMachine - https://docs.docker.com/engine/install/ubuntu/
DockerCompose - https://docs.docker.com/compose/install/
Npm - Ubuntu: sudo apt install npm

## Starting the application
- minikube start
- minikube addons enable ingress
- kubectl get pods -n ingress-nginx (verify you have ingress)
- ./build-and-deploy.sh (you will need to login to dockerhub)
- kubectl get ingress
- Navigate to the url in a browser

## Useful commands

### Base64 Encode
- echo -n 'username' | base64
- echo -n 'password' | base64

### Kubernetes dashboard in minikube
- minikube tunnel
- minikube service --url mongo-express-service
- minikube service mongo-express-service
- Note that without minikube tunnel, kubernetes would be showing external IP as "pending".
- https://minikube.sigs.k8s.io/docs/handbook/accessing/

## Debugging services inside the cluster

### Prerequisites
- Install Telepresence: https://www.telepresence.io/docs/latest/install/
- How to intercept: https://www.telepresence.io/docs/latest/howtos/intercepts/
- telepresence connect
- curl -ik https://kubernetes.default
- telepresence list (find the service you want to intercept)

### Connect api
- telepresence intercept api --port 3000 --env-file ~/backend-service-intercept.env
- Open backend-service-intercept.env and find values to set in env:
- export ME_CONFIG_MONGODB_ADMINUSERNAME=$ME_CONFIG_MONGODB_ADMINUSERNAME';
- export ME_CONFIG_MONGODB_ADMINPASSWORD=$ME_CONFIG_MONGODB_ADMINPASSWORD';
- export ME_CONFIG_MONGODB_SERVER=$MONGODB_SERVICE_SERVICE_HOST;
- From api run: npm run dev

### Connect frontend
- telepresence intercept frontend --port 3001 --env-file ~/frontend-service-intercept.env
- From frontend run: npm run dev

### Disconnect
- telepresence leave service-name

## TODO

- Create scripts to start teleprecense
- Configure the name to guess
