FROM        amazoncorretto:21

LABEL       author="SSdaRealest" maintainer="ssdarealeast@proton.me"
LABEL       org.opencontainers.image.source="https://github.com/ssdarealest/amazon-corretto-pterodactyl"
LABEL       org.opencontainers.image.licenses="MIT"

RUN         yum upgrade -y \
    && yum install -y curl ca-certificates openssl git tar sqlite fontconfig freetype libstdc++.so.6 freetype-devel lsof build-essential tzdata iproute \
    git gcc gcc-c++ automake make libtool \
    && yum clean all \
    && rm -rf /var/cache/yum \
    && useradd -m -d /home/container container

ENV         LC_ALL=en_US.UTF-8
ENV         LANG=en_US.UTF-8
ENV         LANGUAGE=en_US.UTF-8

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container
EXPOSE      25565

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
