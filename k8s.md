# Update Homebrew and Install HyperKit and Minikube
```
brew update
brew install hyperkit minikube
```

# Verify installations
```
hyperkit --version
minikube version
```

# Start and Manage Minikube
```
minikube start --vm-driver=hyperkit
minikube status
minikube delete
minikube start --vm-driver=hyperkit --v=7 --alsologtostderr
minikube status
```

# Basic kubectl Get Commands (Default namespace)
```
kubectl get nodes
kubectl get pods
kubectl get services
kubectl get deployment
kubectl get replicaset
```

# Creating Deployments
```
kubectl create deployment nginx-depl --image=nginx
kubectl create deployment mongo-depl --image=mongo
```

# Authorization Checks (Can I...)
```
kubectl auth can-i create deployments --namespace default
kubectl auth can-i delete nodes --namespace default
```

# Deleting Deployments
```
kubectl delete deployment nginx-depl
kubectl delete deployment mongo-depl
```

# Editing and Applying Configurations
```
vim nginx-deployment.yaml
kubectl apply -f nginx-deployment.yaml
kubectl edit deployment nginx-depl
```

# Debugging and Logging 
# (Replace {pod-name} with actual pod name and {container-name} if pod has multiple containers)
```
kubectl logs {pod-name} -c {container-name}
kubectl describe pod {pod-name}
kubectl exec -it {pod-name} -- /bin/bash
```

# Copying Files to/from Pods
# Copy file from local machine to a pod
```
kubectl cp /path/to/local/file {pod-name}:/path/to/destination
```

# Copy file from a pod to local machine
```
kubectl cp {pod-name}:/path/to/file /path/to/local/destination
```
# Performance Metrics
```
kubectl top nodes
kubectl top pods
```

# Cleanup with Configuration File
```
kubectl delete -f nginx-deployment.yaml
```
