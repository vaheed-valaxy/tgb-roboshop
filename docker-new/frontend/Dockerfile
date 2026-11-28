FROM nginx:1.24.0-alpine3.17-slim

# Remove default Nginx configuration and static content
RUN rm -rf /usr/share/nginx/html/* && \
    rm -f /etc/nginx/nginx.conf && \
    rm -f /etc/nginx/conf.d/default.conf

# Create Nginx directories and configure permissions
RUN mkdir -p /var/cache/nginx/client_temp && \
    mkdir -p /var/cache/nginx/proxy_temp && \
    mkdir -p /var/cache/nginx/fastcgi_temp && \
    mkdir -p /var/cache/nginx/uwsgi_temp && \
    mkdir -p /var/cache/nginx/scgi_temp && \
    mkdir -p /etc/nginx/ssl && \
    chown -R nginx:nginx /var/cache/nginx && \
    chown -R nginx:nginx /etc/nginx && \
    chown -R nginx:nginx /var/log/nginx && \
    touch /var/run/nginx.pid && \
    chown nginx:nginx /var/run/nginx.pid

# Copy custom Nginx configuration with correct ownership
COPY --chown=nginx:nginx nginx.conf /etc/nginx/nginx.conf

# Ensure Nginx configuration is readable
RUN chmod 644 /etc/nginx/nginx.conf && \
    chmod -R 755 /etc/nginx/ssl

# Copy frontend static files
COPY --chown=nginx:nginx static/ /usr/share/nginx/html/

# Run Nginx as non-root user
USER nginx

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
