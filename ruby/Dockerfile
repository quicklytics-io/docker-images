ARG BASE_IMG_VERSION=3.2.2-slim
FROM ruby:${BASE_IMG_VERSION}

ARG RUNTIME_PACKAGES="tini postgresql-client libjemalloc2"

ENV APP_DIR=/app APP_USERNAME=app DEBIAN_FRONTEND=noninteractive

# Allow to use YJIT compiler
# See: https://github.com/ruby/ruby/blob/master/doc/yjit/yjit.md
ENV RUBY_YJIT_ENABLE=1

# create app user
RUN groupadd -g 1000 ${APP_USERNAME} && \
    adduser --uid 1000 --gid 1000 ${APP_USERNAME}

# install runtime dependencies
# hadolint ignore=DL3018
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install --no-install-recommends -y ${RUNTIME_PACKAGES} patchelf && \
    patchelf --add-needed libjemalloc.so.2 /usr/local/bin/ruby && \
    apt-get purge patchelf -y &&\
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR ${APP_DIR}

ENTRYPOINT ["tini", "--"]
