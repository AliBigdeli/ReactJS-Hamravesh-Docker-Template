# build environment
FROM node:lts-alpine as build

ENV NODE_ENV production

WORKDIR /usr/src/app

COPY ./app .

RUN npm install
RUN npm run build

# production environment
FROM nginx:stable-alpine

COPY --from=build /usr/src/app/build /usr/share/nginx/html
COPY ./dockerfiles/prod/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
