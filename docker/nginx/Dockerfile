FROM nginx:1.17.8

ADD ./server.conf /etc/nginx/conf.d/default.conf
WORKDIR /var/www

RUN apt-get update && \
    apt-get install -y vim && \
    apt-get install -y curl