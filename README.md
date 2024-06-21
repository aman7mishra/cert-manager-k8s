# Cert Manager on Kubernetes

This repository provides the necessary files and instructions to install Cert Manager in a Kubernetes cluster. Cert Manager automates the creation and renewal of SSL/TLS certificates, ensuring secure communication between your services.

## Prerequisites

Before you begin, make sure you have:
- A running Kubernetes cluster (v1.16 or newer)
- `kubectl` installed and configured to interact with your cluster
- Private key for your SSL/TLS certificate

## Installation Steps

### Step 1: Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/aman7mishra/cert-manager-k8s.git
cd cert-manager-installation
```

### Step 2: Create a Namespace

Create a dedicated namespace for Cert Manager

```bash
kubectl create namespace cert-manager
```

### Step 3: Create a TLS Secret

A TLS secret is required to store your certificates securely. The `tls-secret.yaml` file defines this secret. Below command creates the secret on Kubernetes. Replace the `data.tls.key` with your private key.

```bash
kubectl apply -f tls-secret.yaml
```

### Step 4: Install Cert Manager

Install Cert Manager using the official YAML manifest

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.15.0/cert-manager.yaml
```

### Step 5: Verify the Installation

Verify that all Cert Manager components are up and running

```bash
kubectl get pods --namespace cert-manager
```

### Step 6: Create a ClusterIssuer

A ClusterIssuer is a resource in Cert Manager that defines how certificates will be obtained. The `clusterissuer.yaml` file defines the Issuer. Below command creates the ClusterIssuer on Kubernetes. Replace the `spec.acme.email` with your CA registered email and replace `spec.acme.solvers.http01.ingress.class` with your ingress class.

```bash
kubectl apply -f clusterissuer.yaml
```

## Conclusion
By following these steps, you have successfully installed Cert Manager in your Kubernetes cluster and configured it to manage SSL/TLS certificates automatically. Cert Manager will now handle the creation, renewal, and management of your certificates, ensuring your services remain secure with minimal manual intervention.

For more advanced setups and configurations, refer to the [Cert Manager documentation](https://cert-manager.io/docs/).

