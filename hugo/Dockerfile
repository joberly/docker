FROM alpine:3.11

# Variables

ARG HUGO_VER=0.64.1
ARG HUGO_TGZ=hugo_${HUGO_VER}_Linux-64bit.tar.gz
ARG HUGO_URL=https://github.com/gohugoio/hugo/releases/download/v${HUGO_VER}/${HUGO_TGZ}
ARG HUGO_UID=1001

# Install tools

RUN apk add --no-cache curl gzip tar

# Install hugo

RUN set -x && \
    HUGO_TMP_DIR=$(mktemp -d) && \
    cd $HUGO_TMP_DIR && \
    mkdir hugo && \
    curl -OL $HUGO_URL && \
    tar -C hugo -xzvf $HUGO_TGZ && \
    install hugo/hugo /usr/local/bin && \
    cd - && \
    rm -rf $HUGO_TMP_DIR

# Remove tools

RUN apk del curl gzip tar

# Create a user for running hugo

RUN adduser -D -u $HUGO_UID hugo

USER hugo
WORKDIR /home/hugo

ENTRYPOINT [ "/usr/local/bin/hugo" ]
CMD [ "help" ]
