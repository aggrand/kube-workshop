# 🌐 Basic Networking

Pods are both ephemeral and "mortal", they should be considered effectively transient.
Kubernetes can terminate and reschedule pods for a whole range of reasons, including rolling updates, hitting resource limits, scaling up & down and other cluster operations.
With Pods being transient, you can not build a reliable architecture through addressing Pods directly (e.g. by name or IP address).

Kubernetes solves this with _Services_, which act as a network abstraction over a group of pods, and have their own lifecycle.
We can use them to greatly improve what we've deployed.

## 📡 Creating a Service

```bash
cat > service.yaml <<EOF
apiVersion: v1
kind: Service
metadata:
  name: echo-server 
spec:
  type: NodePort
  selector:
    app: echo-server
  ports:
  - protocol: TCP
    port: 80
EOF
```

Now we can create the Service:

```bash
kubectl apply -f service.yaml
```

## 🌍 Expose the Server Externally

Ask minikube to open a tunnel and background the job:
```bash
minikube -p "kube-workshop" service echo-server &
```

Query the endpoint minikube gives you:
```bash
curl "http://127.0.0.1:<YOUR_PORT>/param?query=kubernetes-test-query"
```

## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../03-deployment/readme.md) ‖ [Next Section ⏩](../05-improvements/readme.md)
