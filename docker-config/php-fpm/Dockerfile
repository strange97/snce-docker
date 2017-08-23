FROM php:7.1-fpm

# Install selected extensions and other stuff

RUN apt-get update && apt-get install -y \
		apt-utils \
        libfreetype6-dev \
		libjpeg-dev \
		libpng12-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libyaml-dev \
        libbz2-dev \
        libicu-dev \
        libxml2-dev \
        libxslt-dev \
        imagemagick \
        libmagickwand-dev \
		libicu52 \
		zlib1g \
		git
		
RUN docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  docker-php-ext-install -j${NPROC} gd
  
RUN docker-php-ext-install -j$(nproc) iconv mcrypt pdo_mysql bcmath bz2 intl mbstring soap xsl zip

RUN pecl install redis \
        && pecl install xdebug \
        && pecl install imagick \
        && docker-php-ext-enable redis xdebug
		
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
    
RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
    
RUN mkdir /var/symfony && chown -R www-data:www-data /var/symfony && chmod -R 777 /var/symfony

WORKDIR "/application"
