# ---------- Build Stage ----------
FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

# Accept build argument for API URL
ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

COPY . .
RUN npm run build

# ---------- Run Stage ----------
FROM nginx:alpine

# Copy built static files
COPY --from=build /app/dist /usr/share/nginx/html

# Copy custom nginx config that listens on $PORT
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Cloud Run will send PORT=8080 by default
ENV PORT=8080

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
