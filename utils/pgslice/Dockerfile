FROM ghcr.io/quicklytics-io/ruby:3.2.2-alpine

ARG DEV_PACKAGES="postgresql-dev build-base"
ARG PGSLICE_VERSION="0.6.0"

# hadolint ignore=DL3018,DL3028
RUN apk update && \
    apk --no-cache add --virtual build-dependencies $DEV_PACKAGES && \
    gem install pgslice -v ${PGSLICE_VERSION} && \
    apk del build-dependencies

ENTRYPOINT ["tini", "--", "pgslice"]
