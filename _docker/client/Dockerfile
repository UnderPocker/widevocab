ARG NODE_VERSION=21

FROM node:${NODE_VERSION}-alpine AS builder
ENV NODE_OPTIONS="--max-old-space-size=4096"
WORKDIR /app
RUN apk add --no-cache libc6-compat
COPY ../../app ./
RUN yarn install && yarn build


FROM nginx:alpine
WORKDIR /
COPY --from=builder /app/dist /usr/share/nginx/html
COPY ../../_docker/client/nginx.conf /etc/nginx
EXPOSE 8080
ENTRYPOINT ["nginx", "-g", "daemon off;"]