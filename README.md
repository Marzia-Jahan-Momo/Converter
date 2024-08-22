# Python Microservices Converter Application

This repository contains the code for a Python-based microservices application designed for conversion purposes. It includes services for notifications, gateway, conversion, and authentication. Each service is containerized with Docker and deployable using Helm charts on Kubernetes.

## Microservices Overview

### Notification Service
- **Description**: Handles sending notifications to users.
- **Location**: `converter/src/notification-service/`
- **Docker Image**: `docker pull jahanmomo19/py-converter:notification-service`

### Gateway Service
- **Description**: Serves as an API gateway to route requests to the appropriate services.
- **Location**: `converter/src/gateway-service/`
- **Docker Image**: `docker pull jahanmomo19/py-converter:gateway-service`

### Converter Service
- **Description**: Performs the conversion operations.
- **Location**: `converter/src/converter-service/`
- **Docker Image**: `docker pull jahanmomo19/py-converter:converter-service`

### Auth Service
- **Description**: Handles user authentication and authorization.
- **Location**: `converter/src/auth-service/`
- **Docker Image**: `docker pull jahanmomo19/py-converter:auth-service`

## Getting Started

### Prerequisites
1. **Install Docker**: Ensure Docker is installed on your local machine. [Docker Installation Guide](https://docs.docker.com/get-docker/)

2. **Install Kubernetes**: You need a Kubernetes cluster (local or cloud-based). [Kubernetes Installation Guide](https://kubernetes.io/docs/setup/)

3. **Install Helm**: Helm is required for managing Kubernetes applications. [Helm Installation Guide](https://helm.sh/docs/intro/install/)

4. **Install Required Helm Charts**: 
   Navigate to the ```Helm_charts``` directory and follow the instructions in the `README.md` file to install MongoDB, PostgreSQL, and RabbitMQ:

   ```bash
   cd converter/Helm_charts

   # Install MongoDB
   helm install mongodb ./mongodb

   # Install PostgreSQL
   helm install postgresql ./postgresql

   # Install RabbitMQ
   helm install rabbitmq ./rabbitmq
   ```

   For detailed instructions, refer to the `README.md` file in the `Helm_charts` directory.


## Clone the Repository

   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```

## Apply the manifest file for each microservice:

- Auth Service:
```
cd auth-service/manifest

kubectl apply -f .
```
- Gateway Service:

```
cd gateway-service/manifest

kubectl apply -f .
```

- Converter Service:
```
cd converter-service/manifest

kubectl apply -f .
```
- Notification Service:
```
cd notification-service/manifest

kubectl apply -f .
```

- Application Validation
``` 
After deploying the microservices, verify the status of all components by running:

kubectl get all
```

## API Definition
- Login Endpoint

```
POST http://nodeIP:30002/login

```

```
curl -X POST http://nodeIP:30002/login -u <email>:<password>

Expected output: success!
```

- Upload Endpoint

```
POST http://nodeIP:30002/upload
```
```
curl -X POST -F 'file=@./video.mp4' -H 'Authorization: Bearer <JWT Token>' http://nodeIP:30002/upload
```
- Check if you received the ID on your email.

Download Endpoint
```
GET http://nodeIP:30002/download?fid=<Generated file identifier>
```

```
curl --output video.mp3 -X GET -H 'Authorization: Bearer <JWT Token>' "http://nodeIP:30002/download?fid=<Generated fid>"
```

