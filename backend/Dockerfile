# ---------- Stage 1: Build ----------
FROM node:18-alpine AS builder

WORKDIR /app

# Copy only package files first (better caching)
COPY package*.json ./

# Install dependencies (include dev deps for build)
RUN npm ci

# Copy source code
COPY . .

# If you have a build step (TypeScript, webpack, etc.)
# RUN npm run build


# ---------- Stage 2: Production ----------
FROM node:18-alpine AS runner

WORKDIR /app

# Set prod environment
ENV NODE_ENV=production

# Copy only needed files from builder
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules ./node_modules

# If you have a build output, copy that instead of full src
# COPY --from=builder /app/dist ./dist

# Otherwise, copy app source
COPY --from=builder /app ./

# Expose backend port
EXPOSE 5000

# Run prod script
CMD ["npm", "run", "prod"]
