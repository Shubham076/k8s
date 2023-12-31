
# Kubernetes User Configuration Guide

## Introduction

This guide outlines the steps for setting up a new user in a Kubernetes cluster. This includes generating a private key, creating a Certificate Signing Request (CSR), submitting the CSR to the cluster, and configuring `kubectl` with the new credentials.

## Prerequisites

-   Access to a terminal or command line interface.
-   `openssl` installed for certificate generation.
-   `kubectl` installed for interacting with the Kubernetes cluster.

## Steps

### Step 1: Create a Private Key

Generate a private key using OpenSSL.

```
openssl genrsa -out [user-name].key 2048
``` 

### Step 2: Create a Certificate Signing Request (CSR)

Use the private key to create a CSR with your user details.

```
openssl req -new -key [user-name].key -out [user-name].csr -subj "/CN=[user-name]/O=[group]"
``` 

### Step 3: Submit and Approve CSR

Submit the CSR to your Kubernetes cluster. This is typically done by creating a CSR object in Kubernetes.

Create a file named `[user-name]-csr.yaml` with the following content:

```
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: [user-name]
spec:
  request: $(cat [user-name].csr | base64 | tr -d '\n')
  signerName: kubernetes.io/kube-apiserver-client
  usages:
    - client auth
``` 

Apply this configuration to your Kubernetes cluster:
```
kubectl apply -f [user-name]-csr.yaml
``` 

Approve the CSR in Kubernetes (to be done by an administrator):
```
kubectl certificate approve [user-name]
``` 

### Step 4: Retrieve the Approved Certificate

Extract the approved certificate from Kubernetes.

```
kubectl get csr [user-name] -o jsonpath='{.status.certificate}' | base64 --decode > [user-name].crt
``` 

### Step 5: Set User Credentials in kubectl

Configure `kubectl` to use the new user's credentials.

```
kubectl config set-credentials [user-name] --client-certificate=[path/to/user-name.crt] --client-key=[path/to/user-name.key] --embed-certs=true
``` 

### Step 6: Set the Context

Set the context to use these credentials.

```
kubectl config set-context [user-name] --cluster=[cluster-name] --user=[user-name]
```

### Step 7: Test the Configuration

Test to ensure the new user can access the cluster.

```
kubectl --context [user-name] get pods
kubectl config use-context [context-name]
``` 

## Conclusion

Following these steps will help you create a new user in the Kubernetes cluster and configure `kubectl` for accessing the cluster with the new user credentials.
