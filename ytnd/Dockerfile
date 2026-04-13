FROM        --platform=$TARGETOS/$TARGETARCH python:3.12-slim-bookworm

LABEL       author="H1ghSyst3m" maintainer="durmazmalik@protonmail.com"

RUN         apt-get update \
            && apt-get install -y --no-install-recommends \
                git \
                gcc \
                g++ \
                ca-certificates \
                dnsutils \
                curl \
                iproute2 \
                ffmpeg \
                procps \
                tini \
            && curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
            && apt-get install -y --no-install-recommends nodejs \
            && apt-get clean \
            && rm -rf /var/lib/apt/lists/* \
            && useradd -m -d /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL  SIGINT

COPY        --chown=container:container ./entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT  ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]