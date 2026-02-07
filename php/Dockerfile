FROM rgielen/monast-php-docker

USER root

ADD monast-php.zip /
RUN rm -rf /monast-php \
      && unzip monast-php.zip \
      && chgrp -R www-data /monast-php \
      && rm monast-php.zip

ADD config-template.php /

ENV PYMON_HOST=localhost
ENV PYMON_PORT=5039
ENV MONAST_LANGUAGE=en

EXPOSE 80