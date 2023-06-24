# 🏃 Getting Up and Running

Deploying Kubernetes can be extremely complex, with many networking, compute and other aspects to consider.
However for the purposes of this workshop, we will use Minikube to easily set up a local environment.

## 🚀 Deploy a Minikube Cluster
Start a Minikube cluster:
```bash
minikube start -p "kube-workshop"
```

Enable the Minikube metrics server and restart. This will come in handy for the autoscaler later:
```bash
minikube addons enable -p kube-workshop metrics-server
minikube stop
minikube start
```

Ensure that the cluster is up:
```bash
minikube status -p "kube-workshop"
```

Set the default profile:
```bash
minikube profile kube-workshop
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

This pod should be in the ready state. We can view the logs:
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

Expose the pod with a port-forward in the background of the shell:
```bash
kubectl port-forward echo-server-test 3000:80 &
```

Make a request to the pod:
```bash
curl "localhost:3000/param?query=kubernetes-test-query"
```

Clean up by ending the port forward and deleting the pod:
```bash
kill $! # Kill the most recent backgrounded job in this shell.
kubectl delete pod echo-server-test
```

The request fails now:
```bash
curl "localhost:3000/param?query=kubernetes-test-query"
```

## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../01-containers/readme.md) ‖ [Next Section ⏩](../03-deployment/readme.md)
