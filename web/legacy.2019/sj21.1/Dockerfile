FROM ubuntu:18.04
MAINTAINER Seok Joon Lee <seokjoon@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

## nginx & php
RUN apt-get update && apt-get -y install php7.2 php7.2-fpm php7.2-gd php7.2-mysql mysql-client php7.2-curl php7.2-xml php-mbstring php-zip php-imagick nginx && apt-get clean
RUN rm /etc/nginx/sites-available/default
ADD default /etc/nginx/sites-available/default

CMD ["/bin/bash", "-c", "/usr/sbin/service php7.2-fpm start && nginx -g 'daemon off;'"]

EXPOSE 80
EXPOSE 443
EXPOSE 6001