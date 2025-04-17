FROM node:14-slim AS build

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

FROM alpine:3.16

# Install node and npm
RUN apk add --no-cache nodejs npm

WORKDIR /app

COPY --from=build /usr/src/app /app

EXPOSE 3000

CMD ["npm", "start"]
