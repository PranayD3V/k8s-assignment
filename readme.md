# Docker Compose to Kubernetes Manifests

This project demonstrates how to convert a Docker Compose deployment to Kubernetes manifests. The application consists of four services: Frontend, Backend, PostgreSQL, and pgAdmin.

## Application Details

- **Frontend:** Python (Flask)
- **Backend:** Python (Flask)
- **Database:** PostgreSQL
- **Database Management:** pgAdmin

## Prerequisites

- Docker
- `kubectl`
- `kind` (Kubernetes in Docker)

## Setting Up kind Kubernetes Cluster

### Step 1: Install kind

Follow the instructions to install kind from the official documentation: [kind Installation](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

### Step 2: Create a kind Configuration File

Create a file named `kind-config.yaml` with the desired cluster configuration.

### Step 3: Create the kind Cluster

Run the following command to create the kind cluster:

```bash
kind create cluster --config kind-config.yaml
```

### Step 4: Verify the Cluster

Ensure that the cluster is up and running by checking the nodes:

```bash
kubectl get nodes
```

## Kubernetes Setup

### Step 1: Create Namespace

Create a namespace for the application:

```bash
kubectl create namespace my-app
```

### Step 2: Create ConfigMap

Create a ConfigMap for the environment variables and apply it:

```bash
kubectl apply -f configmap.yaml
```

### Step 3: Create Secrets

Create a Secret for sensitive data and apply it:

```bash
kubectl apply -f secret.yaml
```

### Step 4: Create PersistentVolume and PersistentVolumeClaim

Create a PersistentVolume and PersistentVolumeClaim for PostgreSQL and apply them:

```bash
kubectl apply -f pv-pvc.yaml
```

### Step 5: Create Deployments

Create deployments for the Frontend, Backend, PostgreSQL, and pgAdmin services and apply them:

```bash
kubectl apply -f frontend-deployment.yaml
kubectl apply -f backend-deployment.yaml
kubectl apply -f postgres-deployment.yaml
kubectl apply -f pgadmin-deployment.yaml
```

### Step 6: Create Services

Create services for the Frontend, Backend, PostgreSQL, and pgAdmin services and apply them:

```bash
kubectl apply -f frontend-service.yaml
kubectl apply -f backend-service.yaml
kubectl apply -f postgres-service.yaml
kubectl apply -f pgadmin-service.yaml
```

### Step 7: Create Horizontal Pod Autoscaler

Create a Horizontal Pod Autoscaler for the Backend service and apply it:

```bash
kubectl apply -f hpa.yaml
```

## Accessing the Application

### Frontend

Access the Frontend service using the following URL:

```text
http://localhost:<frontend-service-port>
```

### pgAdmin

Access the pgAdmin service using the following URL:

```text
http://localhost:<pgadmin-service-port>
```


By following these steps, you should be able to set up and deploy the application on a kind Kubernetes cluster.
