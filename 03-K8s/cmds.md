# Installation

## Links


[Docker](https://docs.docker.com/engine/install/)
[Kubectl](https://kubernetes.io/docs/tasks/tools/)
[Minikube](https://kubernetes.io/docs/tasks/tools/)
[Kubectl cheat sheet](https://kubernetes.io/docs/reference/kubectl/quick-reference/)


## Start the minikube cluster
1st start VM >> then single node k8s cluster start.


```bash
minikube start
```


## See nodes same as docker ps

```bash
kubectl get nodes
```

## Important Message
[Pods](https://kubernetes.io/docs/concepts/workloads/pods/)

```md
> Pod is a yaml file
```

## Create the Pod
```bash
kubectl create -f pod_file_name.yml
```

## See the running pods
```bash
kubectl get pods
```
* For more details

```bash
kubectl get pods -o wide
```

## Login to cluster
```bash
minikube ssh
```

## Expose cluster
```bash
curl ip_address
```

## Delete the pod
```bash
kubectl delete pod pod_name
```

## Troubleshoot method / See pod logs
```bash
kubectl logs pod_name
```

## Status of the pod / Describe
```bash
kubectl describe pod podname
```

---
*Diagrams generated for personal study notes.*
















