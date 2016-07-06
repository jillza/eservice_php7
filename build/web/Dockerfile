FROM ubuntu:16.04

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y unzip \
    && apt-get clean -y

RUN apt-get -y install apache2 \
    && apt-get -y install php7.0 libapache2-mod-php7.0 \
    && apt-get -y install php-apcu \
    && apt install php-pear -y \
    && apt-get install php-dev -y 

    # Oracle instantclient

ADD instantclient-basic-linux.x64-12.1.0.2.0.zip /tmp/
ADD instantclient-sdk-linux.x64-12.1.0.2.0.zip /tmp/

RUN unzip /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip -d /usr/local/ \
    && unzip /tmp/instantclient-sdk-linux.x64-12.1.0.2.0.zip -d /usr/local/

RUN ln -s /usr/local/instantclient_12_1 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/libclntsh.so.12.1 /usr/local/instantclient/libclntsh.so
RUN ln -s /usr/local/instantclient/libnnz12.so /usr/local/instantclient/libnnz.so

RUN apt-get install libaio-dev -y
RUN echo 'instantclient,/usr/local/instantclient' | pecl install oci8

ADD oci8.ini /etc/php/7.0/apache2/conf.d/
ADD php.ini /etc/php/7.0/apache2/

RUN service apache2 restart 

EXPOSE 80

# By default, simply start apache.
CMD /usr/sbin/apache2ctl -D FOREGROUND