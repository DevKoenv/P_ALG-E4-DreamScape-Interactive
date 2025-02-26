FROM oven/bun:debian

ENV PATH="~/.bun/bin:${PATH}"
RUN ln -s /usr/local/bin/bun /usr/local/bin/node

# Update packages
RUN apt-get update

# Install dependencies
RUN apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    sqlite3 \
    libsqlite3-dev \
    zip \
    unzip \
    supervisor \
    apt-transport-https \
    lsb-release \
    ca-certificates

# Add Sury PHP repository for PHP 8.2
RUN curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
RUN apt-get update

# Install PHP 8.2 and required extensions
RUN apt-get install -y \
    php8.2 \
    php8.2-cli \
    php8.2-fpm \
    php8.2-common \
    php8.2-curl \
    php8.2-mbstring \
    php8.2-sqlite3 \
    php8.2-xml \
    php8.2-zip \
    php8.2-bcmath \
    php8.2-gd

# Set PHP 8.2 as default
RUN update-alternatives --set php /usr/bin/php8.2

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /workspace

# Set environment variables for Laravel
ENV COMPOSER_ALLOW_SUPERUSER=1
ENV COMPOSER_MEMORY_LIMIT=-1

EXPOSE 8000