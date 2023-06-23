# 🐋 Containers

Containers provide a _fast_ and _secure_ way to run an application.

> 📝 NOTE: You may or may not need to prepend docker commands with sudo.

## 🚀 Pull and Run a Container

We're going to use a pre-built image. Pull the image from the official Docker registry:

```bash
docker pull docker/whalesay
```

User `docker run` to spawn a container and execute a command inside it:
```bash
docker run docker/whalesay cowsay "hello kube workshop"
```

In this example, `docker/whalesay` is the image tag, and `cowsay "hello kube workshop"` is the command run inside the container.

The container is removed after execution finishes:
```bash
docker container ls
```

## 🐚 Enter a Container
We're going to spawn a container and open a shell into it:
```bash
docker run -it --entrypoint bash docker/whalesay
```
The `-it` flags ensure we have an interactive TTY and `--entrypoint` overrides the default entrypoint.

Look around inside the container with `ls` and `cd`. Notice that you're now in a different filesystem. Use `ps` and `whoami` to observe the fact that you're a different user and have a different process namespace.

Observe that you're now in an Ubuntu system:
```bash
lsb_release -a
```

You can confirm the fact that the `cowsay` binary is present:
```bash
which cowsay
```

You can run `cowsay` again:
```bash
cowsay "wow I'm inside a container"
```

When you're ready, just exit the shell:
```bash
exit
```

## 🤓 Extras
- The `docker/whalesay` image we used is stored [here](https://hub.docker.com/r/docker/whalesay/). You can see the `Dockerfile` used to build it at the bottom. It specifies `ubuntu:14.04` as the base image, and adds more files (like the `cowsay` binary) in higher layers.
  - You can build an image with the [docker build](https://docs.docker.com/engine/reference/commandline/build/) command.
  - The Dockerfile reference is [here](https://docs.docker.com/engine/reference/builder/). I think of it as a build system like CMake or `go build`.
- The containers we ran in these exercises terminated. Containers used for apps might not terminate.
  - You can see running containers with `docker container ls`
  - You can run a new command inside an existing container with [docker exec](https://docs.docker.com/engine/reference/commandline/exec/).
  - You can remove a container with [docker rm](https://docs.docker.com/engine/reference/commandline/rm/)

## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../00-pre-reqs/readme.md) ‖ [Next Section ⏩](../02-container-registry/readme.md)
