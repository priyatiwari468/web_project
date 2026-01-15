# Backend Dockerfile
FROM node:18-alpine

# Install wget for healthcheck
RUN apk add --no-cache wget

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production && npm cache clean --force

# Copy source code
COPY . .

# Build TypeScript
RUN npm install typescript ts-node @types/node --save-dev && \
    npm run build && \
    npm prune --production

# Expose port
EXPOSE 7000

# Start the application
CMD ["npm", "start"]
