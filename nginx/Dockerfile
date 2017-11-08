FROM nginx:alpine

MAINTAINER Mahmoud Zalt <mahmoud@zalt.me>

ADD nginx.conf /etc/nginx/

ARG PHP_UPSTREAM_CONTAINER=php-fpm
ARG PHP_UPSTREAM_PORT=9000

<<<<<<< HEAD
# fix a problem--#397, change application source from dl-cdn.alpinelinux.org to aliyun source.
# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories

=======
>>>>>>> 714b95199bd2cd89fde315ee724f47480820eb0d
RUN apk update \
    && apk upgrade \
    && apk add --no-cache bash \
    && adduser -D -H -u 1000 -s /bin/bash www-data

# Set upstream conf and remove the default conf
RUN echo "upstream php-upstream { server ${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}; }" > /etc/nginx/conf.d/upstream.conf \
    && rm /etc/nginx/conf.d/default.conf

# install openssl
RUN apk add --no-cache openssl

# create a folder for the keys
RUN mkdir /etc/nginx/ssl 2> /dev/null

# generate the keys for your local domain
RUN openssl genrsa -out "/etc/nginx/ssl/bda.local.key" 2048 \
    && openssl req -new -key "/etc/nginx/ssl/bda.local.key" -out "/etc/nginx/ssl/bda.local.csr" -subj "/CN=bda.local/O=BigDataAgency/C=UK" \
    && openssl x509 -req -days 365 -in "/etc/nginx/ssl/bda.local.csr" -signkey "/etc/nginx/ssl/bda.local.key" -out "/etc/nginx/ssl/bda.local.crt"

CMD ["nginx"]

EXPOSE 80 443
