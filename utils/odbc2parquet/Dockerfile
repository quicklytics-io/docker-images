ARG UBUNTU_VERSION=23.04

FROM ubuntu:${UBUNTU_VERSION} as builder

ARG TOOL_VERSION=2.0.4

RUN apt-get update && \
  apt-get install -y wget && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Download extract and move to PATH somewhere
RUN wget https://github.com/pacman82/odbc2parquet/releases/download/v${VERSION}/odbc2parquet-x86_64-ubuntu.gz -O /tmp.odbc2parquet.gz && \
  gunzip /tmp.odbc2parquet.gz && \
  mv /tmp.odbc2parquet /usr/local/bin/odbc2parquet && \
  rm -rf /tmp/*

FROM ubuntu:${UBUNTU_VERSION}

COPY --from=builder /usr/local/bin/odbc2parquet /usr/local/bin/odbc2parquet

RUN chmod +x /usr/local/bin/odbc2parquet

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install --no-install-recommends -y libodbc2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER 1000

ENTRYPOINT ["/usr/local/bin/odbc2parquet"]
