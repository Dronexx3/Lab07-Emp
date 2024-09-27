# Utilizar la imagen de Node.js 18 en su versión ligera
FROM node:18-slim AS base_image

# Instalar curl y tini para la verificación de salud
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl tini && \
    rm -rf /var/lib/apt/lists/*

# Establecer el directorio de trabajo para la aplicación
WORKDIR /usr/local/app

# Instalar nodemon globalmente para el desarrollo local (monitoreo de archivos)
RUN npm install -g nodemon

# Copiar los archivos de configuración del paquete
COPY package*.json ./

RUN npm install

# Instalar las dependencias y limpiar la caché de npm
RUN npm ci && \
    npm cache clean --force && \
    mv /usr/local/app/node_modules /node_modules

# Copiar el resto del código fuente de la aplicación
COPY . .

# Definir el puerto de la aplicación
ENV PORT 80
# Exponer el puerto 80 para conexiones
EXPOSE 80

# Establecer el punto de entrada con tini y definir el comando a ejecutar
ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["node", "server.js"]
