# Usar una imagen base ligera de Python 3.11 para empezar
FROM python:3.11-slim AS base_stage

# Instalar curl para el chequeo de salud del contenedor
RUN apt-get update && apt-get install -y curl --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# Establecer el directorio de trabajo de la aplicación
WORKDIR /app

# Copiar y proceder a instalar las dependencias desde requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache -r /app/requirements.txt

# Crear una etapa de desarrollo con soporte para cambios en tiempo real
FROM base_stage AS development_stage
RUN pip install watchdog
ENV FLASK_ENV=development
CMD ["python", "app.py"]

# Crear la etapa de producción donde se empaqueta la aplicación
FROM base_stage AS production_stage

# Transferir el código fuente al contenedor
COPY . /app

# Exponer el puerto 80 para las conexiones
EXPOSE 80

# Comando para ejecutar la aplicación usando Gunicorn en producción
CMD ["gunicorn", "--bind", "0.0.0.0:80", "app:app", "--log-file=-", "--access-logfile=-", "--workers=4", "--keep-alive=0"]
