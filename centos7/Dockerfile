FROM centos:7

ENV PATH="/usr/local/bin:${PATH}" \
    CPPFLAGS="-I/usr/include/openssl11" \
    LDFLAGS="-L/usr/lib64/openssl11 -Wl,-rpath=/usr/lib64/openssl11"

RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* && \
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-* && \
    yum -y install epel-release && \
    yum -y update && \
    yum -y install \
        wget gcc gcc-c++ make \
        openssl openssl-devel openssl11 openssl11-devel \
        zlib-devel bzip2-devel readline-devel sqlite-devel libffi-devel \
        xz-devel tk-devel gdbm-devel ncurses-devel libuuid-devel \
        python3 && \
    yum clean all

WORKDIR /usr/src

RUN wget -O Python-3.11.9.tgz https://www.python.org/ftp/python/3.11.9/Python-3.11.9.tgz && \
    tar xzf Python-3.11.9.tgz && \
    cd Python-3.11.9 && \
    ./configure --with-openssl=/usr --with-ensurepip=install && \
    make -j"$(nproc)" && \
    make altinstall && \
    cd /usr/src && \
    rm -rf Python-3.11.9 Python-3.11.9.tgz && \
    ln -sf /usr/local/bin/python3.11 /usr/bin/python3 && \
    ln -sf /usr/local/bin/pip3.11 /usr/bin/pip3

CMD ["sleep", "infinity"]