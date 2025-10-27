FROM salesforce/cli:latest-full

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install --assume-yes openjdk-17-jdk-headless jq python3 python3-requests
RUN apt-get autoremove --assume-yes \
    && apt-get clean --assume-yes \
    && rm -rf /var/lib/apt/lists/*

ENV SF_CONTAINER_MODE true
ENV SFDX_CONTAINER_MODE true
ENV DEBIAN_FRONTEND=dialog
ENV SHELL /bin/bash

#RUN  mkdir -p /app /home/heroku && chown heroku:heroku /app /home/heroku
#USER heroku:heroku

USER root
RUN usermod -l func heroku && \
    groupmod -n func heroku && \
    usermod -d /home/func -m func && \
    mkdir -p /app /home/func && chown func:func /app /home/func

USER func:func

RUN echo y | sf plugins install lightning-flow-scanner@v5.7.1 && \
    echo y | sf plugins install sfdx-git-delta@v6.16.0

ENV SFDX_DISABLE_AUTOUPDATE=true \
    SFDX_DISABLE_TELEMETRY=true \
    SF_DISABLE_AUTOUPDATE=true \
    SF_DISABLE_TELEMETRY=true

WORKDIR /app
