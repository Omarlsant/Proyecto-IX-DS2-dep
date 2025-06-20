FROM node:20-slim AS builder
WORKDIR /app
COPY client/package.json client/package-lock.json ./
RUN npm ci
COPY client/ ./
# Vite usará .env.production automáticamente durante el build
RUN npm run build

FROM nginx:stable-alpine
COPY client/nginx.conf.template /etc/nginx/templates/default.conf.template
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80