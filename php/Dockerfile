FROM php:8.3-cli-alpine

# Install MySQL PDO extension
RUN docker-php-ext-install pdo pdo_mysql

# Set working directory
WORKDIR /workspace/php

# Expose port
EXPOSE 1090

# Start PHP built-in server
CMD ["php", "-S", "0.0.0.0:1090", "-t", "/workspace/php"]
