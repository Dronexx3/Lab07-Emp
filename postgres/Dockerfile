# Empezar con la imagen base de PostgreSQL oficial
FROM postgres:15-alpine AS base_image

# Establecer las variables de entorno para la configuración de PostgreSQL (opcional)
ENV POSTGRES_USER=postgres \
    POSTGRES_PASSWORD=postgres \
    POSTGRES_DB=votingapp

# Hacer accesible el puerto de PostgreSQL
EXPOSE 5432

# Definir un comando de entrada, se puede personalizar si es necesario
CMD ["postgres"]
