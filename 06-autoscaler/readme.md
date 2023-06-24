# ⚖️ Horizontal Pod Autoscaler (HPA)

We've configured an app with 3 pods, but this may be inefficient. A burst of users may require more pods, and when there are few users we don't need many pods. We can configure a horizontal pod autoscaler (HPA) to change the pod count in response to resource utilization.

## 📍 Remove the Replica Count
The HPA will manage our replica count for us, so we can delete it from the Deployment spec:

```bash
cat > deployment-without-replicas.yaml <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  name: echo-server
  labels:
    app: echo-server
spec:
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
        resources:
          requests:
            cpu: 50m
            memory: 50Mi
          limits:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 80
EOF
```

Now we can update the Deployment by applying the new manifest:

```bash
kubectl apply -f deployment-without-replicas.yaml
```

## 🐟 Add the Autoscaler
We will create an autoscaler that will target 50% CPU utilization. We will require there to be at least 1 pod, and will prohibit more than 10 pods. Create the manifest:

```bash
cat > autoscaler.yaml <<EOF
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: echo-server
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: echo-server
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 10
EOF
```

Now we can update the Deployment by applying the new manifest:

```bash
kubectl apply -f autoscaler.yaml
```

After a few seconds you can see the conditions of the autoscaler:
```bash
kubectl describe hpa echo-server
```
It should say that the desired count is within acceptable range, i.e. no scaling needed.

## 🏋️ Load Test
Since we aren't stressing the server, we should still see only one pod:
```bash
kubectl get pods
```

Generate a little load by running the `hey` load generator, just to see how it works:
```bash
hey -z 1s -m GET "http://127.0.0.1:<YOUR_PORT>/api/health"
```

Generate a LOT of load and send the job to the background:
```bash
hey -z 500s -m GET "http://127.0.0.1:<YOUR_PORT>/api/health" &
```

View the status of the HPA:
```bash
kubectl get hpa echo-server
```

View the increased pod count:
```bash
kubectl get pods
```

## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../05-improvements/readme.md) ‖ [Next Section ⏩](../07-extra-advanced/readme.md)
