# Stage 1: Build the Angular application
FROM node:20.15.1-alpine as build

WORKDIR /app

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the Angular app
RUN npm run build --omit=dev

# Stage 2: Serve the app with Nginx
FROM nginx:1.27-alpine

# Copy the built Angular app from the previous stage
COPY --from=build /app/dist/payoneer/browser /usr/share/nginx/html

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]