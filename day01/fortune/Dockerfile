# We are using node23
FROM node:23

LABEL maintainer="chuk"

## Build the application
# we create a directory /app
WORKDIR /app
# we are inside /app

# Copy the files and directories
COPY main.js .
COPY *.json .
COPY public public
COPY views views

# install the dependencies
RUN npm ci
# make sure that I have curl command
RUN apt update && apt install -y curl

## Run the application
ENV APP_PORT=3000

# add healthcheck
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
   CMD curl -s http://localhost:${APP_PORT}/health || exit 1

EXPOSE ${APP_PORT}

SHELL [ "/bin/sh", "-c" ]

ENTRYPOINT node main.js
