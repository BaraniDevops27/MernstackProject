# -------- Stage 1: Build --------
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

# -------- Stage 2: Runtime --------
FROM node:18-alpine

WORKDIR /app

# Security → non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY --from=builder /app /app

USER appuser

EXPOSE 3000

CMD ["node", "server.js"]
