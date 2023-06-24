# ✨ Improving The Deployment

We've cut more than a few corners so far in order to simplify things and introduce concepts one at a time, now is a good time to make some simple improvements.

## 🌡️ Resource Requests & Limits

We have not given Kubernetes any information on the resources (CPU & memory) our applications require, but we can do this two ways:

- **Resource requests**: Used by the Kubernetes scheduler to help assign _Pods_ to a node with sufficient resources.
  This is only used when starting & scheduling pods, and not enforced after they start.
- **Resource limits**: _Pods_ will be prevented from using more resources than their assigned limits.
  These limits are enforced and can result in a _Pod_ being terminated. It's highly recommended to set limits to prevent one workload from monopolizing cluster resources and starving other workloads.

You can specify resources of these within the pod template inside the Deployment YAML. The `resources` section needs to go at the same level as `image`, `ports`, etc. in the spec.

```bash
cat > deployment-with-resources.yaml <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  name: echo-server
  labels:
    app: echo-server
spec:
  replicas: 3
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
kubectl apply -f deployment-with-resources.yaml
```

## 💓 Readiness & Liveness Probes

Probes are Kubernetes' way of checking the health of your workloads. There are two main types of probe:

- **Liveness probe**: Checks if the _Pod_ is alive, _Pods_ that fail this probe will be **_terminated and restarted_**
- **Readiness probe**: Checks if the _Pod_ is ready to **_accept traffic_**, _Services_ only sends traffic to _Pods_ which are in a ready state.

```bash
cat > deployment-with-probes.yaml <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  name: echo-server
  labels:
    app: echo-server
spec:
  replicas: 3
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
        readinessProbe:
          httpGet:
            port: 80
            path: /healthz
          initialDelaySeconds: 1
          periodSeconds: 5
        livenessProbe:
          httpGet:
            port: 80
            path: /healthz
          initialDelaySeconds: 1
          periodSeconds: 5
EOF
```

Now we can update the Deployment by applying the new manifest:
```bash
kubectl apply -f deployment-with-probes.yaml
```

Now that there is a nonzero initial delay, you may be able to notice the rolling update, where pods are replaced one at a time. If you have trouble observing this, increase `initialDelaySeconds` to 10 and try again.

## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../04-network-basics/readme.md) ‖ [Next Section ⏩](../06-autoscaler/readme.md)
