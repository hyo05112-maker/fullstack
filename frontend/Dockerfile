# Render에서는 frontend를 Static Site로 배포하므로 이 파일은 docker-compose 로컬 실행용이다.
FROM node:20-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
# compose에서는 nginx가 /api를 프록시하므로 비워 둔다
ARG VITE_API_URL=""
ENV VITE_API_URL=$VITE_API_URL
RUN npm run build

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
