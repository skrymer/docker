FROM resin/rpi-raspbian:wheezy
LABEL maintainer Sonni Nielsen
 
WORKDIR /opt/rabbit

RUN apt-get update \
    && apt-get install -y erlang logrotate erlang-nox wget

RUN /bin/bash -c 'wget http://www.rabbitmq.com/releases/rabbitmq-server/v3.1.5/rabbitmq-server_3.1.5-1_all.deb' \
    && dpkg -i rabbitmq-server_3.1.5-1_all.deb   

CMD rabbitmq-plugins enable rabbitmq_management &&  rabbitmq-server start
