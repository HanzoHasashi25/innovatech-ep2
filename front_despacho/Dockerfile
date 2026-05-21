# ETAPA 1: Construcción
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# ETAPA 2: Producción (Nginx)
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

COPY --from=builder /app/dist .

RUN touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid /var/cache/nginx /var/log/nginx /etc/nginx
USER nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]