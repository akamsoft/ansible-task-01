FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive \
    PATH="/usr/local/bin:${PATH}"

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential wget curl ca-certificates \
    libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev \
    libffi-dev liblzma-dev tk-dev uuid-dev xz-utils python3 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src

RUN wget -O Python-3.11.9.tgz https://www.python.org/ftp/python/3.11.9/Python-3.11.9.tgz && \
    tar xzf Python-3.11.9.tgz && \
    cd Python-3.11.9 && \
    ./configure --with-ensurepip=install && \
    make -j"$(nproc)" && \
    make altinstall && \
    cd /usr/src && \
    rm -rf Python-3.11.9 Python-3.11.9.tgz && \
    ln -sf /usr/local/bin/python3.11 /usr/bin/python3 && \
    ln -sf /usr/local/bin/pip3.11 /usr/bin/pip3

CMD ["sleep", "infinity"]