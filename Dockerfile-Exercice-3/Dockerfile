FROM node:alpine AS build-front

WORKDIR /app/front

COPY front/package*.json ./

RUN apk update && apk upgrade && \
    npm install 

COPY front/. .





CMD ["npm","run", "build"]

#BACKEND

FROM node:alpine AS backend

WORKDIR /app/backend

COPY back/package*.json ./
COPY back/index.js ./
COPY front/dist/ ./public/
COPY --from=build-front /app/front/dist ./public

RUN apk update && apk upgrade && \
    npm install 

RUN addgroup nodeapp && \
    adduser nodeapp -G nodeapp -s /bin/bash/ -D && \
    adduser unicorn -G nodeapp -s /bin/bash/ -D


RUN chmod -R 755 * && \
    chown -R nodeapp:nodeapp *


EXPOSE 8080

USER nodeapp

CMD ["npm","run", "start"]