FROM centos:latest

ONBUILD RUN yum -y update

# Setup the repo for right version of centos
RUN curl 'https://setup.ius.io/' -o setup-ius.sh && bash setup-ius.sh

# Install common packages
RUN yum -y install php \
			php-fpm \
			php-common \
			php-cli \
			php-curl \
			php-bcmath \
			php-gd \
			php-intl \
			php-json \
			php-mbstring \
			php-mcrypt \
			php-mysqlnd \
			php-opcache \
			php-pdo \
			php-xml \
			php-xmlrpc \
			php-pecl-imagick \
			php-pear \
			php-pecl-zendopcache \
			gcc \
			httpd-devel \
			pcre-devel

# User permissions
RUN useradd nginx

# Opcache (useful for wordpress)
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=60'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /etc/php.d/opcache-recommended.ini

# PHP FPM configuration
COPY ./php-fpm.conf /etc/php-fpm.d/www.conf
COPY ./php.ini /etc/php.ini

EXPOSE 9000

CMD ["php-fpm"]