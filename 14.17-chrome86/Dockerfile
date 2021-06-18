# docker build -t hrcarsan/node:14.17-chrome86 .

FROM hrcarsan/ubuntu:20.04-xvfb
LABEL maintainer="hrcarsan@gmail.com"

RUN export DEBIAN_FRONTEND=noninteractive \
 && apt-get update -y \
 ## install dependencies
 && apt-get install -y --no-install-recommends libcurl3-gnutls libcurl3-nss libcurl4 \
 # Install Google Chrome
 # Note: Check available versions here
 #   https://www.ubuntuupdates.org/package/google_chrome/stable/main/base/google-chrome-stable
 && cd /tmp \
 && export VERSION=86.0.4240.183-1 \
 && wget \https://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_${VERSION}_amd64.deb \
 && dpkg -i google-chrome-stable_${VERSION}_amd64.deb \
 && rm google-chrome-stable_${VERSION}_amd64.deb

ENV DISPLAY :99

RUN apt-get install xz-utils \
 && cd /tmp \
 && export NODE_VERSION=14.17.0 \
 && wget https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz \
 && tar xvf node-v$NODE_VERSION-linux-x64.tar.xz \
 && rm node-v$NODE_VERSION-linux-x64.tar.xz \
 && mv node-v$NODE_VERSION-linux-x64 /opt/ \
 && update-alternatives --install /usr/bin/node node /opt/node-v$NODE_VERSION-linux-x64/bin/node 1 \
 && update-alternatives --install /usr/bin/npm npm /opt/node-v$NODE_VERSION-linux-x64/bin/npm 1 \
 && update-alternatives --install /usr/bin/npx npx /opt/node-v$NODE_VERSION-linux-x64/bin/npx 1

RUN groupadd --gid 1000 node \
    && useradd --uid 1000 --gid node --shell /bin/bash --create-home node

# With this image you can use the next command to run a script that open google-chrome
#  command: bash -c "Xvfb :99 -screen 0 1024x768x16 -ac -nolisten tcp -nolisten unix & node ./dist/app.js"
