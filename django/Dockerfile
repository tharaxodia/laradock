FROM python:3.6

ENV PYTHONUNBUFFERED 1

RUN apt-get update

RUN apt-get install -y python3-icu icu-devtools libicu-dev libicu52 wget

RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code/