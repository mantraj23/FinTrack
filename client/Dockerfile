# Build stage
FROM node:18-alpine as builder

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build   # output goes to /app/dist

# Nginx stage
FROM nginx:alpine

# Copy our custom nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf

# Copy build output to nginx html dir
COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
