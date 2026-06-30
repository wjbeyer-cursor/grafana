# Toolchain image for Cursor Cloud Agents.
# Pins the versions Grafana expects: Go (go.mod), Node (.nvmrc), Yarn (package.json),
# plus GCC for CGo/SQLite compilation of the backend.
FROM ubuntu:24.04

ARG GO_VERSION=1.26.4
ARG NODE_VERSION=24.11.0

ENV DEBIAN_FRONTEND=noninteractive

# build-essential provides GCC, required for CGo/SQLite when building the backend.
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        ca-certificates \
        curl \
        git \
        xz-utils \
    && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL "https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz" -o /tmp/go.tgz \
    && tar -C /usr/local -xzf /tmp/go.tgz \
    && rm /tmp/go.tgz

RUN curl -fsSL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.xz" -o /tmp/node.tar.xz \
    && tar -C /usr/local --strip-components=1 -xJf /tmp/node.tar.xz \
    && rm /tmp/node.tar.xz

ENV PATH="/usr/local/go/bin:/root/go/bin:${PATH}"

# Yarn is managed via corepack and pinned by the repo's packageManager field.
RUN corepack enable
