########################################################################
## FIRST IMAGE (inter) ##
########################################################################
ARG BASE
FROM ${BASE} as inter ## base is node:18-debian
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /workspace/source/

COPY package*.json ./
RUN npm install
COPY . .

RUN npm run build

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

COPY --from=builder /app/dist .

USER 1000

EXPOSE PORTS

CMD ["node", "index.js"]
