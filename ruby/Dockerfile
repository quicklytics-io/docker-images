ARG BASE_IMG_VERSION=3.2.2-alpine
FROM ruby:${BASE_IMG_VERSION}

ENV APP_DIR=/app APP_USERNAME=app

# create app user
RUN addgroup -g 1000 -S ${APP_USERNAME} && \
    adduser -u 1000 -S ${APP_USERNAME} -G ${APP_USERNAME} -s /bin/bash

ARG RUNTIME_PACKAGES="tini"

# install runtime dependencies
# hadolint ignore=DL3018
RUN apk update && \
    apk --no-cache add $RUNTIME_PACKAGES

WORKDIR ${APP_DIR}

ENTRYPOINT ["/usr/bin/tini", "--"]
