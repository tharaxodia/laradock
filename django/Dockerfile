FROM ubuntu:16.04

MAINTAINER Pitipong Guntawong <pppstudio.gm@gmail.com>

ARG PUID=1001
RUN usermod -u $PUID -s /bin/bash www-data && groupmod -g $PUID www-data

#python
RUN apt-get update;
RUN apt-cache search libicu
RUN apt-get install -y icu-devtools libicu-dev libicu55 wget sudo software-properties-common python3-software-properties
RUN add-apt-repository ppa:jonathonf/python-3.6
RUN apt-get update
RUN apt-get install -y python3.6 python3.6-dev python3-pip python3-icu python3-tk
RUN pip3 install --upgrade pip
# RUN apt-get install -y python3 python3-pip python3-icu icu-devtools libicu-dev libicu55 wget sudo
RUN pip3 install nltk pythainlp
RUN pip3 install gunicorn
RUN pip3 install numpy
RUN pip3 install scipy
RUN pip3 install pandas
RUN pip3 install dill
RUN pip3 install scikit-learn
RUN pip3 install matplotlib

ENV PYTHONUNBUFFERED 1
RUN mkdir /config
ADD requirements.pip /config/

RUN pip3 install -r /config/requirements.pip

RUN mkdir /opt/src && chown www-data:www-data /opt/src -R
RUN mkdir -p /var/www && chown www-data:www-data /var/www -R

USER www-data

WORKDIR /opt/src
