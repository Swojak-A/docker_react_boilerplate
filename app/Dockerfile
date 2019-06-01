FROM node:10-alpine

WORKDIR /usr/src/app

COPY package.json /usr/src/app/package.json
COPY package-lock.json /usr/src/app/package-lock.json

RUN npm install
RUN npm install -g serve
RUN npm install -g pm2

COPY . /usr/src/app

RUN npm run build