FROM phpdockerio/php73-fpm

RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y php7.3-mysql \
    && rm -rf /var/lib/apt/lists/*