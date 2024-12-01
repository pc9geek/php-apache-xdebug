FROM ubuntu/apache2

# Set working directory
WORKDIR /var/www/html

# Update package list and install required tools and PHP
RUN apt update && \
    apt install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php -y && \
    apt update && \
    apt install -y php libapache2-mod-php php-cli php-pear php-dev make gcc && \
    apt clean

# Install Xdebug via PECL
RUN pecl install xdebug && \
    mkdir -p /etc/php/$(php -r 'echo PHP_MAJOR_VERSION . "." . PHP_MINOR_VERSION;')/apache2/conf.d && \
    echo "zend_extension=$(find /usr/lib/php/ -name xdebug.so)" > /etc/php/$(php -r 'echo PHP_MAJOR_VERSION . "." . PHP_MINOR_VERSION;')/apache2/conf.d/20-xdebug.ini && \
    echo "xdebug.mode=debug" >> /etc/php/$(php -r 'echo PHP_MAJOR_VERSION . "." . PHP_MINOR_VERSION;')/apache2/conf.d/20-xdebug.ini && \
    echo "xdebug.start_with_request=yes" >> /etc/php/$(php -r 'echo PHP_MAJOR_VERSION . "." . PHP_MINOR_VERSION;')/apache2/conf.d/20-xdebug.ini && \
    echo "xdebug.discover_client_host=true" >> /etc/php/$(php -r 'echo PHP_MAJOR_VERSION . "." . PHP_MINOR_VERSION;')/apache2/conf.d/20-xdebug.ini && \
    echo "xdebug.client_port=9003" >> /etc/php/$(php -r 'echo PHP_MAJOR_VERSION . "." . PHP_MINOR_VERSION;')/apache2/conf.d/20-xdebug.ini

# Ensure Apache runs in the foreground to keep the container alive
CMD ["apache2ctl", "-D", "FOREGROUND"]
