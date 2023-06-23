# 🐋 Containers

Containers provide a _fast_ and _secure_ way to run an application.

> 📝 NOTE: You may or may not need to prepend docker commands with sudo.

## 🚀 Pull and Run a Container

We're going to use a pre-built image. Pull the image from the official Docker registry:

```bash
docker pull ealen/echo-server
```

User `docker run` to spawn a container from this image:
```bash
docker run --name echo-server-test -d -p 3000:80 ealen/echo-server
```

Breaking down this command:
- `docker run` - Create a container from an image and run it
- `--name echo-server-test` - The name of the container
- `-d` - Detach the container
- `-p 3000:80` - Bind the port 3000 on the host to port 80 inside the container
- `ealen/echo-server` - The tag identifying the image create a container from

Check that the container is running:
```bash
docker container ls
```

Make a request to the container:
```bash
curl "localhost:3000/param?query=docker-test-query"
```

View the container logs:
```bash
docker logs echo-server-test
```

Clean up by stopping and removing the container:
```bash
docker stop echo-server-test
docker rm echo-server-test
```

## 🐚 Enter a Container
We're going to spawn a container and open a shell into it:
```bash
docker run -it --entrypoint sh ealen/echo-server
```
The `-it` flags ensure we have an interactive TTY and `--entrypoint` overrides the default entrypoint. We have told the container to run the `sh` shell instead of the server.

Look around inside the container with `ls` and `cd`. Notice that you're now in a different filesystem. Use `ps` and `whoami` to observe the fact that you're a different user and have a different process namespace.

When you're ready, just exit the shell:
```bash
exit
```

## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../00-pre-reqs/readme.md) ‖ [Next Section ⏩](../02-container-registry/readme.md)
