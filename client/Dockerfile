FROM node:14-slim AS build
WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

#STAGE 2:

FROM node:14-slim 

WORKDIR /app
COPY --from=build /usr/src/app /app

EXPOSE 3000

CMD ["npm", "start"]