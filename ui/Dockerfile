# ---------- Stage 1: Build ----------
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files first (better caching)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source
COPY . .

# 🔥 FIX: ensure vite is executable
RUN chmod -R +x node_modules/.bin

# Build app
RUN npm run build

# ---------- Stage 2: Nginx ----------
FROM nginx:stable-alpine

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
