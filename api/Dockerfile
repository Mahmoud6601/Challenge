# Step 1: Use an official PHP image with PHP-FPM (FastCGI Process Manager)
FROM php:8.2-fpm

# Step 2: Install system dependencies for building the application and required PHP extensions
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

# Step 3: Set the working directory inside the container
WORKDIR /var/www

# Step 4: Copy Composer (PHP dependency manager) from its official image to the container
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Step 5: Copy the entire project from the host to the working directory inside the container
COPY . /var/www

# Step 6: Install Laravel dependencies without development packages for production optimization
RUN composer install --optimize-autoloader --no-dev

# Step 7: Ensure the correct permissions for the web server user to access project files
RUN chown -R www-data:www-data /var/www

# Step 8: Expose port 8000, which will be used by the Laravel API
EXPOSE 8000

# Step 9: Start the PHP-FPM service when the container starts
CMD ["php-fpm"]
