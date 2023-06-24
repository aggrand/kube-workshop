# 🚀 Creating a Deployment
To manage groups of pods and their scaling, we need a higher level abstraction: Deployments.

## 🗃️ Deploying the Server

```bash
cat > real-deployment.yaml <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  name: echo-server
  labels:
    app: echo-server
spec:
  replicas: 1
  selector:
    matchLabels:
      app: echo-server
  template:
    metadata:
      labels:
        app: echo-server
    spec:
      containers:
      - name: echo-server
        image: ealen/echo-server
        ports:
        - containerPort: 80
EOF
```

Now we can create the Deployment:

```bash
kubectl apply -f real-deployment.yaml
```

Observe the pod that was created from the Deployment:

```bash
kubectl get pods
```

If you delete the pod, the Deployment will create a new one:
```bash
kubectl delete pod YOUR_POD_NAME
kubectl get pods
```

Having one pod is great, but doesn't give us a strong availability guarantee. We can improve this by adding more replicas. Access the manifest in edit mode:
```bash
kubectl edit deployment echo-server
```

Navigate to the line that says `replicas: 1` and increase it to `replicas: 3`.


## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../02-running/readme.md) ‖ [Next Section ⏩](../04-network-basics/readme.md)
