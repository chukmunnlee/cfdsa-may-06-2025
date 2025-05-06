## Build container
FROM golang:1.24-bookworm AS builder

WORKDIR /src

COPY go.* .
COPY *.go .

# produce /src/main
RUN go build -o main .

FROM debian:12.10

LABEL maintainer="chuk"

WORKDIR /app

# install curl
RUN apt update && apt install -y curl

# /src/main -> /app/main
COPY --from=builder /src/main .
COPY public public
COPY templates templates

ENV PORT=3000 INSTANCE_NAME="dov-bear" INSTANCE_HASH=""

# this is optiona
EXPOSE ${PORT}

# this is optiona
VOLUME /app/public
VOLUME /data

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
   CMD curl http://localhost:${PORT}/healthz || exit 1

SHELL [ "/bin/sh", "-c" ]

ENTRYPOINT /app/main


