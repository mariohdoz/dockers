FROM ubuntu:latest

LABEL Name=calculo_fte_wm Version=0.0.1

#hacer que la consola no sea interactiva
ENV DEBIAN_FRONTEND=noninteractive
#--------------------------------

#instalar apache y php
RUN apt-get update
RUN apt-get install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php

RUN apt-get update && \
	apt-get install -y --allow-unauthenticated php7.2 php7.2-mysql php7.2-cli php7.2-gd php7.2-curl php7.2-mbstring php7.2-soap php7.2-xml php7.2-xsl php7.2-zip php-mongodb htop zip iputils-ping && \
	apt-get install -y build-essential
	
RUN apt-get install -y wget && \
    apt-get install -y curl && \
	apt-get install -y nano
	
#-------------------------	
	
#composer, git y node
RUN curl --silent --show-error https://getcomposer.org/installer | php

RUN apt-get install -y git-core openssl libssl-dev python3

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash
RUN apt-get install --yes nodejs

RUN apt-get install -y git
#----------------------

# Cleanup
RUN apt-get update && apt-get upgrade -y && apt-get autoremove -y
#---------------------

#configurar proyecto
EXPOSE 80

ENV APP_HOME /var/www/html

RUN mkdir -p /opt/data/public && \
    rm -r /var/www/html && \
    ln -s /opt/data/public $APP_HOME

WORKDIR /opt/data

CMD php artisan serve --host=0.0.0.0 --port=80 --env=local
