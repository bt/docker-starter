FROM nginx:alpine

MAINTAINER "Bertram Truong" <b@bertramtruong.com>

# Update OS and enable HHVM
RUN apk update && \
    apk upgrade && \
    apk add --no-cache bash openssl && \
    adduser -D -H -u 1000 -s /bin/bash www-data && \
    rm /etc/nginx/conf.d/default.conf

# Generate SSL certificate
RUN mkdir -p '/etc/ssl/bt.dev' && \
    openssl genrsa -out '/etc/ssl/bt.dev/bt.dev.key' 2048 && \
    openssl req -new \
      -subj '/C=AU/ST=Victoria/O=Dev/localityName=Melbourne/commonName=bt.dev/organizationalUnitName=/emailAddress=/' \
      -key '/etc/ssl/bt.dev/bt.dev.key' \
      -out '/etc/ssl/bt.dev/bt.dev.csr' \
      -passin pass:bt_1234 && \
    openssl x509 -req -days 365 -in '/etc/ssl/bt.dev/bt.dev.csr' \
      -signkey '/etc/ssl/bt.dev/bt.dev.key' \
      -out '/etc/ssl/bt.dev/bt.dev.crt'

# Copy configuration in
COPY nginx.conf /etc/nginx/
COPY config/*.conf /etc/nginx/
COPY sites/*.conf /etc/nginx/sites-available/

CMD ["nginx"]

EXPOSE 80 443
