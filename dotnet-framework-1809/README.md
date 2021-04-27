# buildpacks/samples dotnet-framework
Loosely based on dotnet-framework sample builder: https://github.com/buildpacks/samples/blob/main/builders/dotnet-framework/builder.toml

Usage:
```
dockerHostIP="<IP of Docker host (requires insecure-registries entry in daemon.json)>"

docker run --name my-registry --publish 5000:5000 --detach micahyoung/registry

docker build --tag my-build --build-arg appImage=$dockerHostIP:5000/my-app .

docker pull $dockerHostIP:5000/my-app

docker run --rm --publish 8080:80 --interactive --tty $dockerHostIP:5000/my-app
```
