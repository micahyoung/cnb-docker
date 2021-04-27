FROM cnbs/sample-stack-build:alpine

COPY --from=buildpacksio/lifecycle:0.11.1-linux /cnb/lifecycle/ /cnb/lifecycle

COPY --from=cnbs/sample-package:hello-world /cnb/buildpacks/samples_hello-world/0.0.1/ /cnb/buildpacks/samples_hello-world/0.0.1

USER root

RUN mkdir /layers /platform /workspace && \
    chown -R 1000:1000 /workspace && \
    echo 'order = [{ group = [{ id = "samples/hello-world", version = "0.0.1" }] }]' > /cnb/order.toml && \
    echo 'run-image = { image = "cnbs/sample-stack-run:alpine" }' > /cnb/stack.toml

WORKDIR /layers

ARG appImage
RUN /cnb/lifecycle/creator \
    -app=/workspace \
    $appImage
