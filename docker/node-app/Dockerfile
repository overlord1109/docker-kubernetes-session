# LTS image of node 10
FROM node:10

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

# Node app binds to 8080 by default
EXPOSE 8080

# Define the command to run your app -> "node server.js"
CMD [ "node", "server.js" ]
