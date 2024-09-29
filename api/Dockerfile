# Step 1: Use an official PHP image as the base
FROM php:8.2-fpm

# Step 2: Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    locales \
    zip \
    unzip \
    git \
    curl \
    libonig-dev \  
    libzip-dev \  
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo_mysql mbstring exif pcntl bcmath zip

# Step 3: Set working directory
WORKDIR /var/www

# Step 4: Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Step 5: Copy project files
COPY . /var/www

# Step 6: Install Laravel dependencies
RUN composer install --optimize-autoloader --no-dev

# Step 7: Set file permissions
RUN chown -R www-data:www-data /var/www

# Step 8: Expose port 8000 (for API)
EXPOSE 8000

# Step 9: Start PHP-FPM service
CMD ["php-fpm"]
