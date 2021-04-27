FROM alpine AS samples

RUN apk add git && git clone --branch main --single-branch --depth 1 https://github.com/buildpacks/samples

FROM cnbs/sample-stack-build:bionic

USER root

COPY --from=buildpacksio/lifecycle:0.11.1-linux /cnb/lifecycle/ /cnb/lifecycle

COPY --from=samples /samples/buildpacks/java-maven/ /cnb/buildpacks/samples_java-maven/0.0.1

COPY --from=samples /samples/apps/java-maven/ /workspace

RUN mkdir /layers /platform && \
    chown -R 1000:1000 /workspace && \
    echo 'order = [{ group = [{ id = "samples/java-maven", version = "0.0.1" }] }]' > /cnb/order.toml && \
    echo 'run-image = { image = "cnbs/sample-stack-run:bionic" }' > /cnb/stack.toml

WORKDIR /layers

ARG appImage
RUN /cnb/lifecycle/creator \
    -app=/workspace \
    $appImage
