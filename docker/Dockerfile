FROM php:8.2-fpm

# Diretório de trabalho dentro do container
WORKDIR /var/www/html

# Instalação de dependências do sistema para o Laravel
RUN apt-get update --fix-missing && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    zip \
    vim \
    unzip \
    git \
    curl \
    libzip-dev \
    libonig-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Limpa cache e instala extensões PHP para o MySQL
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd

# Instala o Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

EXPOSE 9000
CMD ["php-fpm"]