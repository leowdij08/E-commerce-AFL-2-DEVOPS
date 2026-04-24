# Build stage
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./

# Install dependencies + bersih-bersih cache langsung
RUN npm ci --only=production && \
    npm cache clean --force

COPY . .

# Production stage (lebih ringan)
FROM node:18-alpine

WORKDIR /app

# Copy hanya hasil dari builder stage
COPY --from=builder /app .

# Set environment
ENV NODE_ENV=production
ENV PORT=8080

# Buat user non-root untuk keamanan (opsional tapi recommended)
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

USER nodejs

EXPOSE 8080

CMD ["node", "server.js"]