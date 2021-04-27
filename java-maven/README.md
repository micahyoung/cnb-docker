# buildpacks/samples hello-world
Loosely based on bionic sample builder: https://github.com/buildpacks/samples/blob/main/builders/bionic/builder.toml

Usage:
```
docker run --name my-registry --publish 5000:5000 --detach registry:2

docker build --tag my-build --network=host --build-arg app-image=localhost:5000/my-app .

docker pull localhost:5000/my-app

docker run --rm --publish 8080:8080 localhost:5000/my-app
```
