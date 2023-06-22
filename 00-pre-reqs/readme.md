# ⚒️ Workshop Pre Requisites

As this is a completely hands on workshop, you will need several things before you can start:

- A Linux or up-to-date MacOS machine
- bash or a bash compatible shell (e.g. zsh), please do not attempt to use PowerShell or cmd.
- A good editor, we will mostly be editing yaml files
  - I've heard good things about [Kubernetes extension](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools) for [VS Code](https://code.visualstudio.com/), but have never used it.
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
- [helm](https://helm.sh/docs/intro/install/)

## Install dependencies

Instructions are for MacOS. I assume that Linux users are free spirits who can adapt this for their distro.

### 🐋 Install Docker

If you're using Apple silicon, rosetta is recommended:
```bash
softwareupdate --install-rosetta
```

Using Homebrew:
```bash
brew install --cask docker
```

Without Homebrew, download the dmg [here](https://docs.docker.com/desktop/install/mac-install/).

Go ahead and start the Docker app using the app launcher.

### 🧊 Install Minikube

Using Homebrew:
```bash
brew install minikube
```

Without Homebrew, MacOS x86-64:
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64
sudo install minikube-darwin-amd64 /usr/local/bin/minikube
```

Without Homebrew, MacOS ARM64:
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-arm64
sudo install minikube-darwin-arm64 /usr/local/bin/minikube
```

### Setup Kubectl
Minikube has a built-in kubectl which we can guarantee is up-to-date with the Kubernetes version it runs. For convenience, let's just use that:
```bash
alias kubectl="minikube kubectl --"
```

Ensure that it works:
```bash
kubectl version --client
```

## Navigation

[Return to Main Index 🏠](../readme.md) ‖ [Next Section ⏩](../01-cluster/readme.md)
