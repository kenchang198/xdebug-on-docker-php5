FROM php:5.4-apache

ADD php.ini /usr/local/etc/php/php.ini

# Xdebug setup
RUN BEFORE_PWD=$(pwd) \
    && mkdir -p /opt/xdebug \
    && cd /opt/xdebug \
    && curl -k -L https://github.com/xdebug/xdebug/archive/XDEBUG_2_2_7.tar.gz | tar zx \
    && cd xdebug-XDEBUG_2_2_7 \
    && phpize \
    && ./configure --enable-xdebug \
    && make clean \
    && sed -i 's/-O2/-O0/g' Makefile \
    && make \
    && make install \
    && cd "${BEFORE_PWD}" \
    && rm -r /opt/xdebug
RUN docker-php-ext-enable xdebug

RUN service apache2 restart

EXPOSE 80

CMD ["/usr/sbin/apachectl","-DFOREGROUND"]