FROM ghcr.io/quicklytics-io/ruby:3.2.2-alpine

ARG DEV_PACKAGES="postgresql-dev build-base"
ARG TOOL_VERSION="0.6.1"

# hadolint ignore=DL3018,DL3028
RUN apk update && \
    apk --no-cache add --virtual build-dependencies $DEV_PACKAGES && \
    gem install pgslice -v ${TOOL_VERSION} && \
    apk del build-dependencies

USER app

ENTRYPOINT ["tini", "--", "pgslice"]
