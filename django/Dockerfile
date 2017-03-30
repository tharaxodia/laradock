FROM ubuntu:16.04

MAINTAINER Pitipong Guntawong <pppstudio.gm@gmail.com>

ARG PUID=1001
RUN usermod -u $PUID -s /bin/bash www-data && groupmod -g $PUID www-data

#python
RUN apt-get update;
RUN apt-cache search libicu
RUN apt-get install -y python3 python3-pip python3-icu icu-devtools libicu-dev libicu55 wget
RUN pip3 install nltk pythainlp
RUN pip3 install gunicorn

ENV PYTHONUNBUFFERED 1
RUN mkdir /config
ADD requirements.pip /config/

RUN mkdir /opt/src && chown www-data:www-data /opt/src -R
RUN mkdir -p /var/www && chown www-data:www-data /var/www -R

USER www-data

RUN pip3 install -r /config/requirements.pip



WORKDIR /opt/src