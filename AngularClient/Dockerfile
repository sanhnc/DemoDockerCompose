FROM node:16.14.0-slim AS build
ARG NODE_ENV
ENV NODE_OPTIONS=--max-old-space-size=8192

WORKDIR /app
COPY ./package.json ./
COPY ./package-lock.json ./
RUN npm install
COPY . .
RUN npm run build -- --configuration=production

FROM nginx:1.19.8-alpine
COPY ./backend.nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist/ /usr/share/nginx/html
EXPOSE 80
