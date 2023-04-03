FROM ghcr.io/quicklytics-io/ruby:3.2.2-alpine

ARG DEV_PACKAGES="postgresql-dev build-base"

# hadolint ignore=DL3018
RUN apk update && \
    apk --no-cache add --virtual build-dependencies $DEV_PACKAGES && \
    gem install pgslice && \
    apk del build-dependencies

ENTRYPOINT ["tini", "--", "pgslice"]
