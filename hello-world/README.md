# buildpacks/samples hello-world
Loosely based on alpine sample builder: https://github.com/buildpacks/samples/blob/main/builders/alpine/builder.toml

Usage:
```
docker run --name my-registry --publish 5000:5000 --detach registry:2

docker build --tag my-build-image --network=host --build-arg app-image=localhost:5000/my-app .
```
