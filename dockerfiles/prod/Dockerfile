# build environment
FROM node:lts-alpine as build

# maintainer
LABEL maintainer="bigdeli.ali3@gmail.com"

# making the environment for production mode
ENV NODE_ENV production

# changing working dir
WORKDIR /usr/src/app

# copying the whole project
COPY ./app .

# installing all dependencies
RUN npm install

# building the project
RUN npm run build

# production environment
FROM nginx:stable-alpine

# copying build files and nginx files
COPY --from=build /usr/src/app/build /usr/share/nginx/html
COPY ./dockerfiles/prod/nginx.conf /etc/nginx/conf.d/default.conf

# exposing port 80 to access pages
EXPOSE 80

# runing nginx and putting in loop
CMD ["nginx", "-g", "daemon off;"]
