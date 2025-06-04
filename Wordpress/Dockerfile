FROM wordpress:latest

RUN apt-get update && \
    apt-get install -y ca-certificates curl unzip gnupg2 && \
    update-ca-certificates && \
    curl -o /usr/local/share/ca-bundle.crt https://curl.se/ca/cacert.pem && \
    echo "curl.cainfo = /usr/local/share/ca-bundle.crt" > /usr/local/etc/php/conf.d/curl.ini && \
    echo "openssl.cafile = /usr/local/share/ca-bundle.crt" > /usr/local/etc/php/conf.d/openssl.ini && \
    rm -rf /var/lib/apt/lists/*
