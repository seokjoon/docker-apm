FROM ubuntu:19.04
MAINTAINER Seok Joon Lee <seokjoon@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

## nginx & php
# RUN apt-get update && apt-get -y install php7.2 php7.2-fpm php7.2-gd php7.2-mysql mysql-client php7.2-curl php7.2-xml php-mbstring php-zip php-imagick nginx && apt-get clean
# RUN apt-get update && apt-get -y install php7.2 php7.2-fpm php7.2-gd php7.2-mysql mysql-client php7.2-curl php7.2-xml php-mbstring php-zip php-imagick nginx php-pear php7.2-dev && apt-get clean
RUN apt-get update && apt-get -y install php7.2 php7.2-fpm php7.2-gd php7.2-mysql mysql-client php7.2-curl php7.2-xml php-mbstring php-zip php-imagick nginx php-pear php7.2-dev php7.2-bcmath && apt-get clean
RUN rm /etc/nginx/sites-available/default
ADD default /etc/nginx/sites-available/default
ADD 30-inotify.ini /etc/php/7.2/cli/conf.d/30-inotify.ini
RUN pecl install inotify

## timezone KST
WORKDIR /etc/php/7.2/fpm
RUN sed -i "s/;date.timezone =/date.timezone = Asia\/Seoul/g" php.ini

## upload size
WORKDIR /etc/php/7.2/fpm
RUN sed -i "s/upload_max_filesize = 2M/upload_max_filesize = 11M/g" php.ini
RUN sed -i "s/post_max_size = 8M/post_max_size = 60M/g" php.ini
RUN sed -i "s/max_execution_time = 30/max_execution_time = 300/g" php.ini

## composer
# RUN apt-get -y install curl && apt-get clean && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/bin/composer

## supervisord
# RUN apt-get update && apt-get -y install supervisor && apt-get clean
## RUN supervisorctl start wcmsV3-laravel-article-receive:*
# RUN mkdir -p /var/log/supervisor /etc/supervisor /etc/supervisor/conf.d
# COPY supervisord.conf /etc/supervisor/supervisord.conf
# COPY conf.d/wcmsV3-laravel-article-receive.conf /etc/supervisor/conf.d/wcmsV3-laravel-article-receive.conf
# CMD ["/usr/bin/supervisord -c /etc/supervisor/supervisord.conf"]
## CMD ["/usr/bin/supervisord"]
## RUN supervisorctl start wcmsV3-laravel-article-receive:*

RUN apt-get update && apt-get install -y supervisor && apt-get clean
RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/supervisord.conf
COPY wcmsV3-laravel-article-receive.conf /etc/supervisor/conf.d/wcmsV3-laravel-article-receive.conf

# CMD ["/bin/bash", "-c", "/usr/sbin/service php7.2-fpm start && nginx -g 'daemon off;'"]
CMD ["/usr/bin/supervisord"]
# ADD start.sh /
# RUN chmod +x /start.sh
# CMD ["/start.sh"]


# EXPOSE 80
# EXPOSE 8000
# EXPOSE 8080
# EXPOSE 443
# EXPOSE 6001
