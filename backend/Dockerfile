FROM node:14-slim AS build
WORKDIR /usr/ken/app

COPY package*.json ./
RUN npm install

COPY . .

#stage2

FROM alpine:3.16

RUN apk add --no-cache nodejs npm

WORKDIR /app

COPY --from=build /usr/ken/app /app/

EXPOSE 5000
CMD [ "node", "server.js" ]