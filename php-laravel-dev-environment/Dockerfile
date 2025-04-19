FROM ubuntu:24.10

# Remove CLI interation when downloading packages
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y git curl 

# PHP
RUN apt-get install -y php php-cli php-common php-xml php-pdo php-mbstring php-mysql php-curl php-zip php-gd php-sqlite3 && \
    apt-get clean

RUN php -version

# Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'.PHP_EOL; } else { echo 'Installer corrupt'.PHP_EOL; unlink('composer-setup.php'); exit(1); }" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

RUN mv composer.phar /usr/local/bin/composer
RUN composer --version

# NVM
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash

# Laravel installer
RUN composer global require laravel/installer
ENV PATH="/root/.composer/vendor/bin:${PATH}"
ENV PATH="/root/.config/composer/vendor/bin:${PATH}"

# Code Server
RUN bash -c "source $HOME/.nvm/nvm.sh && nvm install 20"
RUN curl -fsSL https://code-server.dev/install.sh | sh

# Reset CLI interation 
ENV DEBIAN_FRONTEND=dialog

WORKDIR /var/www/html

CMD ["bash", "-c", "nohup code-server --host 0.0.0.0 --port 8080 & exec bash"]

