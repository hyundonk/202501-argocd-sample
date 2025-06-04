# Kubernetes Manifests Repository

This repository contains a collection of Kubernetes manifests for deploying a simple NGINX web application and creating test namespaces.

## Repository Structure

```
.
└── kubernetes/
    └── manifests/
        ├── deployment.yaml
        ├── test-namespace.yaml
        └── test2.yaml
```

## Manifest Descriptions

### deployment.yaml

This manifest contains two Kubernetes resources:

1. **NGINX Deployment**:
   - Deploys 2 replicas of NGINX web server using the `nginx:1.21` image
   - Exposes port 80 within the cluster
   - Runs in the `default` namespace

2. **NGINX Service**:
   - Creates a ClusterIP service named `nginx-service`
   - Routes traffic to pods with the label `app: nginx`
   - Exposes port 80
   - Runs in the `default` namespace

### test-namespace.yaml

Creates a Kubernetes namespace called `test` which can be used for testing and isolation purposes.

### test2.yaml

Creates a Kubernetes namespace called `test2` which can be used as an additional testing environment.

## Usage

### Prerequisites

- Kubernetes cluster (local or remote)
- `kubectl` command-line tool installed and configured to communicate with your cluster

### Applying the Manifests

To create the test namespaces:

```bash
kubectl apply -f kubernetes/manifests/test-namespace.yaml
kubectl apply -f kubernetes/manifests/test2.yaml
```

To deploy the NGINX application:

```bash
kubectl apply -f kubernetes/manifests/deployment.yaml
```

To apply all manifests at once:

```bash
kubectl apply -f kubernetes/manifests/
```

### Accessing the NGINX Service

The NGINX service is exposed as a ClusterIP service, which means it's only accessible within the cluster. To access it from outside the cluster, you can use port-forwarding:

```bash
kubectl port-forward service/nginx-service 8080:80
```

Then access the application at http://localhost:8080

## License

This project is open-source and available under the [MIT License](LICENSE).