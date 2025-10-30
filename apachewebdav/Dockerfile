# Start from the official Apache HTTP Server image
FROM httpd:2.4

# Install required WebDAV modules
RUN apt-get update && apt-get install -y --no-install-recommends \
        apache2-utils \
    && rm -rf /var/lib/apt/lists/*

# Enable WebDAV modules
RUN sed -i '/LoadModule dav_module/s/^#//g' /usr/local/apache2/conf/httpd.conf \
    && sed -i '/LoadModule dav_fs_module/s/^#//g' /usr/local/apache2/conf/httpd.conf \
    && sed -i '/LoadModule dav_lock_module/s/^#//g' /usr/local/apache2/conf/httpd.conf

# Create directories for config and data
RUN mkdir -p /usr/local/apache2/conf/webdav /usr/local/apache2/var/webdav \
    && chown -R www-data:www-data /usr/local/apache2/var/webdav

# Include optional external WebDAV config
RUN echo "IncludeOptional conf/webdav/*.conf" >> /usr/local/apache2/conf/httpd.conf

# Define volumes for config and data
VOLUME ["/usr/local/apache2/conf/webdav", "/usr/local/apache2/var/webdav"]

EXPOSE 80
CMD ["httpd-foreground"]
