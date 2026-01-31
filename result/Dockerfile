# Stage 1: Dependencies
FROM node:18-alpine AS dependencies

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install production dependencies only
RUN npm ci --omit=dev --silent && \
    npm cache clean --force


# Stage 2: Production
FROM node:18-alpine

WORKDIR /app

# Copy prod deps from dependencies stage
COPY --from=dependencies /app/node_modules ./node_modules


# Copy application source code
COPY . .

# Expose port
EXPOSE 3000

# Start the application
CMD ["node", "server.js"]