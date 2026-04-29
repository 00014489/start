# -------------------------
# BUILD STAGE
# -------------------------
FROM node:20 AS build

WORKDIR /app

# Install dependencies first (better caching)
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

# Build Angular app
RUN npm run build

# -------------------------
# RUNTIME STAGE (Nginx)
# -------------------------
FROM nginx:alpine

# Copy build output to nginx
COPY --from=build /app/dist/ /usr/share/nginx/html

# Expose web port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]