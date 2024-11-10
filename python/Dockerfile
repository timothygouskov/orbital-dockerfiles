########################################################################
## FIRST IMAGE (inter) ##
########################################################################
ARG BASE
FROM ${BASE} as inter ## base is python3.11-buster ?
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /workspace/source/

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

RUN pip install --no-cache-dir -r requirements.txt --target .

########################################################################
## SECOND (FINAL) IMAGE ##
########################################################################
FROM ${BASE}
ARG BASE
ARG REPO
ARG PORTS
ARG NPM_VERSION
SHELL ["/bin/bash", "-c"]

WORKDIR /app

COPY --from=inter /app .

USER 1000

EXPOSE PORTS

CMD ["python", "app.py"]


