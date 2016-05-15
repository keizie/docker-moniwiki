FROM ubuntu:14.04
MAINTAINER Daekwon Kim <propellerheaven@gmail.com>

# Install basic packages
RUN \
  apt-get update &&\
  apt-get -qq -y install curl rcs

# Install php5 and apache2
RUN \
  apt-get -qq -y install apache2 php5 libapache2-mod-php5 &&\
  a2enmod rewrite

# Install Moniwiki
WORKDIR /tmp
# Github Version is no wikiseed (use, naver's version)
# or wikiseed from https://github.com/wkpark/moniwiki-wikiseed/archive/master.zip
RUN \
  curl -L -O http://dev.naver.com/frs/download.php/11750/moniwiki-1.2.5.tgz &&\
  tar xf /tmp/moniwiki-1.2.5.tgz &&\
  rm -rf /var/www/html/* &&\
  mv moniwiki/* /var/www/html/ &&\
  mkdir -p /var/www/html/data/text &&\
  mv /var/www/html/wikiseed/ko/* /var/www/html/data/text &&\
  chown -R www-data:www-data /var/www/html/* &&\
  chmod 777 -R /var/www/html/data/ /var/www/html/ &&\
  chmod +x /var/www/html/secure.sh &&\
  /var/www/html/secure.sh

VOLUME /var/www/html/data
VOLUME /var/www/html/pds

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80
CMD bash -c "source /etc/apache2/envvars && /usr/sbin/apache2 -D FOREGROUND"
