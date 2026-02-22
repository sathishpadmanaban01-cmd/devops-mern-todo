# Use Node.js LTS
FROM node:18

# Set working directory
WORKDIR /app

# Copy package files first to leverage Docker cache
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the source code
COPY . .

# Expose backend port
EXPOSE 5000

# Set environment variable (optional)
ENV NODE_ENV=production

# Run the prod script
CMD ["npm", "run", "prod"]