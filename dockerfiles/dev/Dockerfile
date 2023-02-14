FROM node:lts-alpine AS development

ENV NODE_ENV development

# Add a work directory
WORKDIR /usr/src/app

# Copy app files
COPY ./app .

# Cache and Install dependencies
RUN npm install

# Expose port
EXPOSE 3000
