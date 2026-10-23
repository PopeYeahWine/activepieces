# Microsoft development tools retained; effective Node patch selected explicitly.
FROM mcr.microsoft.com/devcontainers/javascript-node:1-22-bookworm@sha256:0d29e5fdc64f8397cd502223e0c4679f1e60877ca0fd2db4f2e2e0028e4271af

ENV NODE_VERSION=22.23.4
RUN su node -c ". /usr/local/share/nvm/nvm.sh && nvm install 22.23.4 && nvm alias default 22.23.4 && nvm uninstall 22.16.0 && nvm cache clear"
ENV PATH="/usr/local/share/nvm/versions/node/v22.23.4/bin:${PATH}"

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=22.23.4
# RUN su node -c "source /usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>"

RUN npm install -g nx
RUN apt-get update && apt-get install -y git

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    locales \
    locales-all \
    libcap-dev \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y poppler-utils poppler-data

# Set the locale
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

COPY default.cf /usr/local/etc/isolate

RUN npm i -g bun@1.3.1 npm@9.9.3 cross-env@7.0.3


# install isolated-vm in a parent directory to avoid linking the package in every sandbox
RUN cd /usr/src && bun i isolated-vm@5.0.1
