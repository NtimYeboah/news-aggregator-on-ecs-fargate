# NPM dependencies

FROM node:24-slim AS npm-build

WORKDIR /var/www/html/

RUN apt-get update && apt-get upgrade -y

COPY package.json package-lock.json tailwind.config.js postcss.config.js vite.config.js /var/www/html/
COPY resources /var/www/html/resources/
COPY public /var/www/html/public/

RUN npm ci
RUN npm run build

# Nginx
FROM nginx:1.29

COPY .docker/nginx/nginx.conf /etc/nginx/conf.d/default.conf
COPY --chown=www-data --from=npm-build /var/www/html/public/ /var/www/html/public/
COPY --chown=www-data . /var/www/html/
