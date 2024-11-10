########################################################################
## FIRST IMAGE (inter) ##
########################################################################
ARG BASE
FROM ${BASE} as inter ## base is ruby:3.2-debian
ARG BASE
ARG REPO
ARG PORTS
SHELL ["/bin/bash", "-c"]

WORKDIR /workspace/source/

COPY Gemfile Gemfile.lock ./
RUN bundle install
COPY . .

RUN bundle exec rails assets:precompile

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

COPY --from=inter /workspace/source .

USER 1000

EXPOSE PORTS

CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]

