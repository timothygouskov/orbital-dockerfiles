########################################################################
## FIRST IMAGE (inter) ##
########################################################################
ARG BASE
FROM ${BASE} as inter ## base is golang:1.23
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /workspace/source/

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN go build -o app .

########################################################################
## SECOND (FINAL) IMAGE ##
########################################################################
FROM ${BASE}
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /app

COPY --from=inter /app/app .

USER 1000

EXPOSE PORTS

CMD ["./app"]
