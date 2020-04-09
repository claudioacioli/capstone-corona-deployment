# capstone-corona-deployment

This is part of the another projects for capstone Udacity CloudDeveloper

## Scheduler

The objective for this deployment is run on kubernetes and docker environments

## Install

To run this make sure you have a Postgres database and Python3 on your machine:

- Execute the [sql](https://raw.githubusercontent.com/claudioacioli/capstone-corona-deployment/master/coronaboard.sql) file to create the database columns
- Clone this project 
```bash
git clone https://github.com/claudioacioli/capstone-coronaboard-deployment.git deploy
```

## Run on Docker
```bash
cd deploy/docker
docker-compose -f docker-compose-build.yaml build --parallel
docker-compose up
```

## Run on Kubernetes Minikube

Make the config files

```bash
cd k8s
kubectl apply -f deploy/k8s/env-config.yaml
kubectl apply -f deploy/k8s/env-secret.yaml
```

Make the deployments

```bash
kubectl apply -f deploy/k8s/backend-country-deployment.yaml
kubectl apply -f deploy/k8s/backend-country-scheduler.yaml
kubectl apply -f reverseproxy-deployment.yaml
```

Make the services

```bash
kubectl apply -f deploy/k8s/backend-country-service.yaml
kubectl apply -f reverseproxy-service.yaml
```

Expose the reverse proxy:

```bash
kubectl port-forward service/reverseproxy 8080:8080
```

