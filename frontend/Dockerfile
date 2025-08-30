# Etapa de construcción
FROM node:18-alpine as build

# Crear directorio de la aplicación
WORKDIR /app

# Copiar package.json y package-lock.json si existe
COPY package*.json ./

# Limpiar caché de npm antes de instalar
RUN npm cache clean --force

# Instalar dependencias con más verbosidad para debug
RUN npm install

# Copiar el resto del código
COPY . .

# Construir para producción
RUN npm run build

# Etapa de producción
FROM nginx:alpine

# Copiar archivos construidos desde la etapa de build
COPY --from=build /app/build /usr/share/nginx/html

# Copiar configuración personalizada de nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Exponer puerto 80
EXPOSE 80

# Comando por defecto
CMD ["nginx", "-g", "daemon off;"]