# Stage 1: Build TypeScript
FROM node:18 AS builder

WORKDIR /app

# Install all dependencies (including devDependencies)
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

# Compile TS -> build/
RUN npm run build

# Stage 2: Run compiled JS
FROM node:18

WORKDIR /app

# Copy only necessary files
COPY --from=builder /app/package*.json ./
RUN npm install --only=production

COPY --from=builder /app/build ./build

EXPOSE 3001
CMD ["node", "build/index.js"]
