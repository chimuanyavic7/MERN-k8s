# ----------------------------
# Stage 1: Build Stage
# ----------------------------
FROM node:20-alpine AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies (only production deps can also be installed here if needed)
RUN npm ci --production

# Copy the rest of the application source code
COPY . .

# ----------------------------
# Stage 2: Production Stage
# ----------------------------
FROM node:20-alpine AS production

# Set working directory
WORKDIR /app

# Copy only necessary files from build stage
COPY --from=build /app ./

# Expose the port your app runs on
EXPOSE 5050

# Start the application
CMD ["node", "server.js"]