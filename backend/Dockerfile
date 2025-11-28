# Use Node LTS
FROM node:18

# Set working directory
WORKDIR /usr/src/app

# Copy package.json and install deps
COPY package*.json ./
RUN npm install --production

# Copy app code
COPY . .

# Expose port
EXPOSE 3000

# Start app
CMD ["node", "server.js"]
