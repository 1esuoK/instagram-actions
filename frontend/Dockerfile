# Stage 1: Build Stage
FROM node:16 AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install

# Copy all other source code
COPY . .

# Stage 2: Production Stage
FROM node:16-alpine
WORKDIR /app

# Copy only the necessary files from the build stage
COPY --from=build /app .

# Ensure no sensitive files are included in the final image
RUN rm -rf /root/.npm/_cacache /path/to/any/sensitive/files

EXPOSE 3000
CMD ["npm", "start"]
