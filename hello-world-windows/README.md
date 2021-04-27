# buildpacks/samples hello-world-windows
Loosely based on nanoserver-1809 sample builder: https://github.com/buildpacks/samples/blob/main/builders/nanoserver-1809/builder.toml

Usage:
```
dockerHostIP="<IP of Docker host (requires insecure-registries entry in daemon.json)>"

docker run --name my-registry --publish 5000:5000 --detach micahyoung/registry

docker build --tag my-build --build-arg appImage=$dockerHostIP:5000/my-app .
```
