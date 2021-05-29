# docker build -t hrcarsan/node:14.17-xvfb .
FROM hrcarsan/ubuntu:20.04-xvfb
LABEL maintainer="hrcarsan@gmail.com"

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

# Using this image you can use the next command to run a script that open a browser for example
#  command: bash -c "Xvfb :99 -screen 0 1024x768x16 -ac -nolisten tcp -nolisten unix & node ./dist/app.js"
