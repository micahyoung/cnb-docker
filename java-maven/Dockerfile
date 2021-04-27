FROM alpine AS samples

RUN apk add curl && \
    curl -o samples.tar.gz -L https://github.com/buildpacks/samples/archive/refs/heads/main.tar.gz && \
    tar -x -f samples.tar.gz -C / && \
    rm samples.tar.gz

FROM cnbs/sample-stack-build:bionic

USER root

COPY --from=buildpacksio/lifecycle:0.11.1-linux /cnb/lifecycle/ /cnb/lifecycle

COPY --from=samples /samples-main/buildpacks/java-maven/ /cnb/buildpacks/samples_java-maven/0.0.1

COPY --from=samples /samples-main/apps/java-maven/ /workspace

RUN mkdir /layers /platform && \
    chown -R 1000:1000 /workspace && \
    echo 'order = [{ group = [{ id = "samples/java-maven", version = "0.0.1" }] }]' > /cnb/order.toml && \
    echo 'run-image = { image = "cnbs/sample-stack-run:bionic" }' > /cnb/stack.toml

WORKDIR /layers

ARG appImage
RUN /cnb/lifecycle/creator \
    -app=/workspace \
    $appImage
