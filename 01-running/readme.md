# 🏃 Getting Up and Running

Deploying Kubernetes can be extremely complex, with many networking, compute and other aspects to consider.
However for the purposes of this workshop, we will use Minikube to easily set up a local environment.

## 🚀 Deploy a Minikube Cluster
Start a Minikube cluster:
```bash
minikube start -p "kube-workshop"
```

Ensure that the cluster is up:
```bash
minikube status -p "kube-workshop"
```

## 🐋 Run a Basic Container

We will create a basic pod and run it to completion. This pod will contain the echo server we explored in a previous exercise.
First, create the kube manifest file:
```bash
cat > basic-pod.yaml <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: echo-server-test
spec:
  containers:
  - name: echo-server-test
    image: ealen/echo-server
EOF
```

Now we can run the pod:

```bash
kubectl apply -f basic-pod.yaml
```

List pods:
```bash
kubectl get pods
```

This pod is in the completed state, since it just printed the logs then exited. We can view the logs:
```bash
kubectl logs echo-server-test
```

Get more info about the pod:
```bash
kubectl describe pod echo-server-test
```

Get the full manifest for the pod:
```bash
kubectl get pod -o yaml echo-server-test
```

Get a shell inside a pod:
```bash
kubectl exec --stdin --tty echo-server-test -- sh
```

Clean up by deleting the pod:
```bash
kubectl delete pod whalesay-test
```

## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../00-pre-reqs/readme.md) ‖ [Next Section ⏩](../02-container-registry/readme.md)
