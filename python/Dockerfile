ARG BASE_IMG_VERSION=3.11.2-slim-bullseye
FROM python:${BASE_IMG_VERSION}

ENV APP_DIR=/app APP_USERNAME=python
ENV PYTHONUNBUFFERED=1 PYTHONDONTWRITEBYTECODE=1 DEBIAN_FRONTEND=noninteractive

ARG RUNTIME_PACKAGES="tini libpq5"
# Install system dependencies
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install --no-install-recommends -y ${RUNTIME_PACKAGES} && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN groupadd -g 1000 ${APP_USERNAME} && \
    useradd -r -u 1000 -g python ${APP_USERNAME}

WORKDIR ${APP_DIR}

ENTRYPOINT ["/usr/bin/tini", "--"]
