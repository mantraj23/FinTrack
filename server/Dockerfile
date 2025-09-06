# Stage 1: Build TypeScript
FROM node:18 AS builder

WORKDIR /app

# Copy package.json and install dependencies (including devDependencies for tsc)
COPY package*.json ./
RUN npm install

# Copy all source files
COPY . .

# Compile TS -> build/
RUN npx tsc -p .

# Stage 2: Run compiled JS
FROM node:18

WORKDIR /app

# Copy package.json & node_modules
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules ./node_modules

# Copy compiled build
COPY --from=builder /app/build ./build

EXPOSE 3001
CMD ["npm", "start"]
