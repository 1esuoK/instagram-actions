# Stage 1: Build Stage
FROM node:16 AS build
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Update npm and install dependencies
RUN npm install -g npm@latest \
    && npm install \
    && npm audit fix

# Copy the remaining source code
COPY . .

# Stage 2: Production Stage
FROM node:16-alpine
WORKDIR /app

# Install necessary packages and update the system libraries
RUN apk update && apk upgrade \
    && apk add --no-cache openssl@3.1.4-r0

# Copy only the necessary files from the build stage
COPY --from=build /app .

# Ensure no sensitive files are included in the final image
RUN rm -rf /root/.npm/_cacache /path/to/any/sensitive/files

EXPOSE 3000
CMD ["npm", "start"]
