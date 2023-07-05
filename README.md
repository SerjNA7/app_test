# app_test

Создайте приложение Node.js

1) Сначала создать новый каталог, в котором будут жить все файлы. В этом каталоге создать файл package.json, который описывает приложение и его зависимости:

{
  "name": "app",
  "version": "1.0.0",
  "description": "Node.js on Docker",
  "author": "nsa <ury_047@inbox.ru>",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}

2) npm install
3) Затем создать файл server.js, который определяет веб-приложение с помощью фреймворка Express.js:

'use strict';

const express = require('express');

// Constants
const PORT = 8080;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('site under construction :)');
});

app.listen(PORT, HOST, () => {
  console.log(`Running on http://${HOST}:${PORT}`);
});


Создание Dockerfile

1) Создать пустой файл под названием Dockerfile:

touch Dockerfile

sudo nano Dockerfile

FROM node:18

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --omit=dev

# Bundle app source
COPY . .

EXPOSE 8080
CMD [ "node", "server.js" ]

2) touch .dockerignore

node_modules
npm-debug.log

Запускаем контейнер

1) sudo docker build . -t app

2) sudo docker run -p 80:8080 -d app
