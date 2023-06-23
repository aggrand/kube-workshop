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

We will create a basic pod and run it to completion. This pod will contain the `whalesay` container we explored in a previous exercise.
First, create the kube manifest file:
```bash
cat > basic-pod.yaml <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: whalesay-test
spec:
  containers:
  - name: cowsay-test
    image: docker/whalesay
    command: ['cowsay', 'hello from kube']
  restartPolicy: Never
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
kubectl logs whalesay-test
```

Get more info about the pod:
```bash
kubectl describe pod whalesay-test
```

Get the full manifest for the pod:
```bash
kubectl get pod -o yaml whalesay-test
```

Clean up by deleting the pod:
```bash
kubectl delete pod whalesay-test
```

## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../00-pre-reqs/readme.md) ‖ [Next Section ⏩](../02-container-registry/readme.md)
