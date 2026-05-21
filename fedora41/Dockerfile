FROM fedora:41

ENV PATH="/usr/local/bin:${PATH}"

RUN dnf -y update && \
    dnf -y install \
        gcc gcc-c++ make \
        wget curl ca-certificates \
        openssl-devel \
        zlib-devel bzip2-devel readline-devel sqlite-devel \
        libffi-devel xz-devel tk-devel gdbm-devel ncurses-devel \
        libuuid-devel \
        python3 \
        && dnf clean all

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