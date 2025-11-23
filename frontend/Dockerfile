# ------------------- Stage 1: Build Stage ------------------------------
    FROM node:21 AS build

    WORKDIR /app
    
    COPY package*.json ./
    RUN npm install
    
    # Copy environment variables BEFORE build
    COPY .env.docker .env
    
    # Copy full project
    COPY . .
    
    # Build Vite dist folder
    RUN npm run build
    
    # ------------------- Stage 2: Serve with Nginx -------------------------
    FROM nginx:alpine
    
    # Copy custom nginx config
    COPY nginx.conf /etc/nginx/conf.d/default.conf
    
    # Copy build output
    COPY --from=build /app/dist /usr/share/nginx/html
    
    EXPOSE 80
    CMD ["nginx", "-g", "daemon off;"]
    