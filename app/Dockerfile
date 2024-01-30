FROM node:13.6.0-alpine

# Create app directory
Run mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./
RUN rm -rf package-lock.json node_modules
RUN npm install

# Ajouter le code source de l'application
COPY . .

USER node
CMD ["npm","start"]