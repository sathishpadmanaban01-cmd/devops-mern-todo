# ---------- Stage 1: Build ----------
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files for caching
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy the rest of the source
COPY . ./

# Build frontend (React / Vue / Angular)
RUN npm run build

# ---------- Stage 2: Serve ----------
FROM node:18-alpine AS runner

WORKDIR /app

# Install a small HTTP server (serve)
RUN npm install -g serve

# Copy built files from builder
COPY --from=builder /app/dist ./dist

# Expose frontend port
EXPOSE 3000

# Run the server
CMD ["serve", "-s", "dist"]
