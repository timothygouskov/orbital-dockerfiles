########################################################################
## FIRST IMAGE (inter) ##
########################################################################
ARG BASE
FROM ${BASE} as inter ## BASE is debian:latest
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /workspace/source/

COPY src/ CMakeLists.txt ./

RUN apt-get update -y && \
    apt-get install -y build-essential cmake && \
    cmake . && \
    make

########################################################################
## SECOND (FINAL) IMAGE ##
########################################################################
FROM ${BASE}
ARG BASE
ARG REPO
ARG PORTS
ARG NPM_VERSION
SHELL ["/bin/bash", "-c"]

COPY --from=inter /workspace/source .

RUN apt-get update -y && \
    apt-get install -y libc++1

USER 1000

EXPOSE PORTS

CMD ["./app"]
