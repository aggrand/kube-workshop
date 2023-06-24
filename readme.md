# Kubernetes Developer Workshop

This is a hands-on, technical workshop intended / hack to get comfortable working with Kubernetes, and
deploying and configuring applications. It was forked from Ben Coleman's [workshop](https://github.com/benc-uk/kube-primer) and heavily modified.

This workshop is very much designed for software engineers & developers with little or zero Kubernetes
experience, but wish to get hands on and learn how to deploy and manage applications.

## The Workshop

This workshop will involve us running an app in Minikube.

Sections / modules:

- [⚒️ Workshop Pre Requisites](00-pre-reqs/readme.md) - Covering the pre set up and tools that will be
  needed.
- [🐋 Containers](01-containers/readme.md) - Run a basic container and explore its internals
- [🏃 Getting Up and Running](02-running/readme.md) - Start Minikube and run a simple pod on it
- [🚀 Creating a Deployment](03-deployment/readme.md) - Introducing Services to provide network access
- [🌐 Basic Networking](04-network-basics/readme.md) - Introducing Services to provide network access
- [✨ Improving The Deployment](05-improvements/readme.md) - Configure resource requests, limits, and probes
- [⚖️ Horizontal Pod Autoscaler (HPA)](06-autoscaler/readme.md) - Set up an autoscaler to handle load

### 📖 Extra Reading & Teach Yourself Exercises

A very brief list of potential topics and Kubernetes features you may want to look at after finishing:

### Kubernetes Features

- [Init containers](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)
- [Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/)
- [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Debugging Pods with shell access and exec](https://kubernetes.io/docs/tasks/debug-application-cluster/get-shell-running-container/)
- Assigning Pods to Nodes with [selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) and [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)
- [Cluster Autoscaler in AKS](https://docs.microsoft.com/azure/aks/cluster-autoscaler)

### Other Projects

- Enable the [Kubernetes dashboard](https://github.com/kubernetes/dashboard)
- Enabling TLS with certificates from Let's Encrypt using [Cert Manager](https://cert-manager.io/docs/)
- Observability
  - With [Prometheus](https://artifacthub.io/packages/helm/prometheus-community/prometheus) & [Grafana](https://artifacthub.io/packages/helm/grafana/grafana)
  - Using [AKS monitoring add-on](https://docs.microsoft.com/azure/azure-monitor/containers/container-insights-overview)
- Using [Dapr](https://dapr.io/) for building portable and reliable microservices
- Adding a service mesh such as [Linkerd](https://linkerd.io/) or [Open Service Mesh](https://docs.microsoft.com/azure/aks/open-service-mesh-about)
- Setting up the [Application Gateway Ingress Controller (AGIC)](https://docs.microsoft.com/azure/application-gateway/ingress-controller-overview)
