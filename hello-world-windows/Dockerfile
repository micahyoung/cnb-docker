FROM cnbs/sample-stack-build:nanoserver-1809

COPY --from=buildpacksio/lifecycle:0.11.1-windows /cnb/lifecycle/ /cnb/lifecycle

COPY --from=cnbs/sample-package:hello-world-windows /cnb/buildpacks/samples_hello-world-windows/0.0.1/ /cnb/buildpacks/samples_hello-world-windows/0.0.1

USER ContainerAdministrator

RUN mkdir c:\layers c:\platform c:\workspace && \
    echo order = [{ group = [{ id = "samples/hello-world-windows", version = "0.0.1" }] }] > c:\cnb\order.toml && \
    echo run-image = { image = "cnbs/sample-stack-run:nanoserver-1809" } > c:\cnb\stack.toml

WORKDIR /layers

ARG appImage
RUN c:\cnb\lifecycle\creator \
    -app=c:\workspace \
    %appImage%
