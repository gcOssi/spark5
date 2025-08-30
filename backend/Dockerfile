# Usar imagen base oficial de Node.js
FROM node:18-alpine

# Crear directorio de la aplicación
WORKDIR /app

# Copiar archivos de dependencias
COPY package*.json ./

# Instalar dependencias
RUN npm ci --only=production

# Copiar código de la aplicación
COPY . .

# Crear usuario no root para seguridad
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nextjs -u 1001

# Cambiar propietario de los archivos
RUN chown -R nextjs:nodejs /app
USER nextjs

# Exponer el puerto
EXPOSE 4000

# Variables de entorno por defecto
ENV NODE_ENV=production
ENV PORT=4000

# Comando para iniciar la aplicación
CMD ["npm", "start"]