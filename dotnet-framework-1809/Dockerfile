FROM mcr.microsoft.com/windows/nanoserver:1809 AS samples

USER ContainerAdministrator

RUN mkdir samples-main && curl -o samples.tar.gz -L https://github.com/buildpacks/samples/archive/refs/heads/main.tar.gz && \
    tar -x -f samples.tar.gz -C c:\ samples-main/buildpacks samples-main/apps && \
    del samples.tar.gz

FROM cnbs/sample-stack-build:dotnet-framework-1809

SHELL ["cmd", "/s", "/v", "/c"]
COPY --from=buildpacksio/lifecycle:0.11.1-windows /cnb/lifecycle/ /cnb/lifecycle

COPY --from=samples /samples-main/buildpacks/dotnet-framework/ /cnb/buildpacks/samples_dotnet-framework/0.0.1

COPY --from=samples /samples-main/apps/aspnet/ /workspace

USER ContainerAdministrator

RUN mkdir c:\layers c:\platform && \
    echo order = [{ group = [{ id = "samples/dotnet-framework", version = "0.0.1" }] }] > c:\cnb\order.toml && \
    echo run-image = { image = "cnbs/sample-stack-run:dotnet-framework-1809" } > c:\cnb\stack.toml

WORKDIR /layers

ARG appImage
RUN c:\cnb\lifecycle\creator \
    -app=c:\workspace \
    %appImage%
