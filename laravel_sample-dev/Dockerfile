# Ivan Medina 
# 19/05/21
# Imagen de Laravel 8 con PHP 7.4 y Valet

FROM ubuntu:20.04
ENV DEBIAN_FRONTEND=noninteractive

# Actualizar ubutnu y dependencias
RUN \
    apt-get -y update --fix-missing && apt-get -y upgrade

# Instalar utilidades para instalar composer
RUN \
    apt install \
        php-cli \
        unzip curl \
    -y

# Instalar librerias necesarias para composer
RUN \
    apt-get install \
        libapache2-mod-php7.4 \
        php7.4-common \
        php7.4-gd \
        php7.4-mysql \
        php7.4-curl \
        php7.4-intl \
        php7.4-xsl \
        php7.4-mbstring \
        php7.4-zip \
        php7.4-bcmath \
        php7.4-soap \
        php-xdebug \
        php-imagick \
    -y

# Instalar utilidades para la red
RUN \
    apt-get install \
        network-manager\
        libnss3-tools\
        jq\
        xsel\
    -y

# Instalar utilidades para debuguear
RUN \
    apt-get install \
        iputils-ping \
        net-tools \
        netcat \
        vim \
    -y

# Crear usuario valet
RUN \
    useradd -rm -d /home/valet -s /bin/bash -g root -G sudo -u 1000 valet

# Instalar composer
RUN cd /home/valet &&\
    curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && HASH=`curl -sS https://composer.github.io/installer.sig` \
    && echo $HASH   \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
ENV HOME="/home/valet"
USER root
RUN \
    cd /home/valet \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer

# Instalar valet
WORKDIR /home/valet
RUN composer global require cpriego/valet-linux
ENV PATH="${PATH}:/home/valet/.config/composer/vendor/bin"

# Crear proyecto laravel
RUN composer create-project laravel/laravel laravel

# Confifurar e iniciar valet (no mapea los puertos correctamente por que no escucha en 0.0.0.0)
RUN valet install && valet park && valet start

# Iniciar artisan en puerto 80 escuchando en 0.0.0.0 (solucion temporal al problema con valet)
WORKDIR /home/valet/laravel
CMD ["./artisan","serve","--port=80", "--host=0.0.0.0"]

EXPOSE 80