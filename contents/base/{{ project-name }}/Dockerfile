FROM node:22-alpine AS builder

# Set up workspace
WORKDIR /app

# Copy application code
COPY . .

# Production stage with nginx
FROM nginx:alpine

# Copy built static files to nginx html directory with proper ownership
COPY --from=builder --chown=nginx:nginx /app/{{ apps-dir }}/ /usr/share/nginx/html/{{ apps-dir }}/

# Copy custom nginx configuration
COPY --from=builder --chown=nginx:nginx /app/nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
# Set hostname to 0.0.0.0 to make it accessible from outside the container
ENV HOSTNAME=0.0.0.0

# Expose the port the app runs on
ENV PORT={{ port }}
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]