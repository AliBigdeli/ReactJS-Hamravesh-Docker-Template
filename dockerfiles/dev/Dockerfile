# getting the latest lts version of node
FROM node:lts-alpine

# mainainer
LABEL maintainer="bigdeli.ali3@gmail.com"

# putting project in dev mode
ENV NODE_ENV development

# Add a work directory
WORKDIR /usr/src/app

# copying packages
COPY ./app/package*.json .

# Cache and Install dependencies
RUN npm install

# Copy app files
COPY ./app .

# Expose port
EXPOSE 3000

# starting the dev server
CMD [ "npm", "start" ]