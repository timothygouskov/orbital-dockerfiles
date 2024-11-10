########################################################################
## FIRST IMAGE (inter) ##
########################################################################
ARG BASE
FROM ${BASE} as inter ## base is openjdk:17-jdk-debian ??
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /workspace/source/

COPY src/ /app/src/
COPY pom.xml /app/

RUN apk add --no-cache --virtual .build-deps \
    maven \
&& mvn package -DskipTests

#######################################################################
## SECOND (FINAL) IMAGE ##
########################################################################
FROM ${BASE}
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /app

COPY --from=inter /app/target/*.jar .

USER 1000

EXPOSE PORTS

CMD ["java", "-jar", "app.jar"]
