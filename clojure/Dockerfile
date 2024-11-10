########################################################################
## FIRST IMAGE (inter) ##
########################################################################
ARG BASE
FROM ${BASE} as inter
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /workspace/source/

COPY project.clj ./
COPY src src/

## TODO - add leiningen as the manager

RUN clojure -T:deploy clojure -M -m deps.deploy

########################################################################
## SECOND (FINAL) IMAGE ##
########################################################################
FROM ${BASE}
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

COPY --from=inter /app/target/my-app.jar app.jar

USER 1000

EXPOSE PORTS

ENTRYPOINT ["java", "-jar", "app.jar"]

