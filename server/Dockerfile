# Stage 1: Build TypeScript
FROM node:18 AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Compile TS -> build/
RUN npm run build

# Stage 2: Run compiled JS
FROM node:18

WORKDIR /app

COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/build ./build

EXPOSE 3001
CMD ["npm", "start"]
