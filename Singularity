BootStrap: docker
From: ubuntu:bionic

%labels
    Author kiwiroy@users-noreply.github.com
    Maintainer kiwiroy@users-noreply.github.com
    Version 1.00

%post
### install / update system dependencies
    apt-get -y update && apt-get -y install \
        autoconf             \
        build-essential      \
        curl                 \
        git                  \
        libbz2-dev           \
        libcurl4-openssl-dev \
        liblz4-dev           \
        liblzma-dev          \
        libssl-dev           \
        libzstd-dev          \
        zlib1g-dev
### install htslib 1.9 due to a dependency
    git clone https://github.com/samtools/htslib.git htslib-1.9
    cd htslib-1.9
    git reset --hard 1832d3a
    autoreconf && ./configure && make -j5 && make install
    cd ..
### install zstd - commented as libzstd-dev installs enough
    # git clone https://github.com/facebook/zstd.git zstd
    # cd zstd
    # make -j5 V=1 && make install V=1
    # cd ..
### clone project
    git clone https://github.com/mklarqvist/tomahawk.git tomahawk
    cd tomahawk
    make -j5 && make install
### update ld.so.cache - avoid setting LD_LIBRARY_PATH for libhts.so
    ldconfig

%runscript
    tomahawk
