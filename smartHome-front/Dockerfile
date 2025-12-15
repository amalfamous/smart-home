FROM node:16-alpine AS builder
WORKDIR /app

# Copier les fichiers de dépendances
COPY package*.json ./

# Installer TOUTES les dépendances (pas seulement production)
RUN npm install

# Copier le reste du code
COPY . .

# Build l'application
RUN npm run build --prod

FROM nginx:alpine
# Copier les fichiers build
COPY --from=builder /app/dist/smart-home /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
