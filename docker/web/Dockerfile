FROM alpine:3.13

ENV APACHE_DOCUMENT_ROOT /var/www/html/web
ENV APACHE_SERVER_NAME localhost
ENV APACHE_HTTP_PORT 8080

RUN apk --no-cache add vim apache2 apache2-proxy

RUN sed -ri -e 's!/var/www/localhost/htdocs!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/httpd.conf \
    && sed -ri -e 's!^#ServerName .*!ServerName ${APACHE_SERVER_NAME}!g' /etc/apache2/httpd.conf \
    && sed -ri -e 's!Listen 80!Listen ${APACHE_HTTP_PORT}!g' /etc/apache2/httpd.conf \
    && sed -ri -e 's!^ErrorLog .*!ErrorLog /proc/self/fd/2!g' /etc/apache2/httpd.conf \
    && sed -ri -e 's!^\s*CustomLog .*!CustomLog /proc/self/fd/1 common!g' /etc/apache2/httpd.conf \
    && sed -ri -e 's!AllowOverride None!AllowOverride All!g' /etc/apache2/httpd.conf \
    && sed -ri -e 's!^#LoadModule rewrite_module!LoadModule rewrite_module!g' /etc/apache2/httpd.conf \
    && echo 'PidFile /run/httpd.pid' >> /etc/apache2/httpd.conf

COPY ./httpd_extra.conf /etc/apache2/conf.d/zz_httpd_extra.conf

WORKDIR /var/www/html
EXPOSE 8080
ENTRYPOINT ["/usr/sbin/httpd", "-DFOREGROUND"]
