# ⚒️ Workshop Pre Requisites

As this is a completely hands on workshop, you will need several things before you can start:

- A Linux or up-to-date MacOS machine
- bash or a bash compatible shell (e.g. zsh), please do not attempt to use PowerShell or cmd.
- [Optional] [Homebrew](https://brew.sh/) makes the dependency setup easier for MacOS.

## 🗄️ Workshop Directory
You should probably create a directory to run all the project commands in, since we'll create a lot of yaml files:
```bash
mkdir ~/kube-workshop
pushd ~/kube-workshop
```

## 📦 Install dependencies

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

If not using Homebrew, download the dmg [here](https://docs.docker.com/desktop/install/mac-install/).

Go ahead and start the Docker app using the app launcher, it can take a while on the first load.

### 🧊 Install Minikube

Using Homebrew:
```bash
brew install minikube
```

If not using Homebrew, MacOS x86-64:
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64
sudo install minikube-darwin-amd64 /usr/local/bin/minikube
```

if not using Homebrew, MacOS ARM64:
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

### Install Hey
We will use the [hey](https://github.com/rakyll/hey) load generator when we experiment with autoscaling.

Using Homebrew:
```bash
brew install minikube
```

If not using Homebrew, MacOS x86-64:
```bash
curl -LO https://hey-release.s3.us-east-2.amazonaws.com/hey_darwin_amd64
mv hey_darwin_amd64 /usr/local/bin/hey
```

If you didn't use Homebrew, you may need to override the MacOS security settings to allow `hey` to run, since Apple considers it an "unidentified developer".

## Navigation

[Return to Main Index 🏠](../readme.md) ‖ [Next Section ⏩](../01-containers/readme.md)
