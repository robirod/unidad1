# Portal de Reserva de Horas Médicas — Proyecto DevOps

Aplicación web estática contenerizada con **Nginx (`nginx:alpine`)** y **Docker Compose** para la gestión simulada de reserva de horas médicas en un entorno local reproducible.

## Estructura del proyecto

```text
proyecto-devops/
├── src/
│   ├── _static/           # Imagenes utilizadas en formulario
│   ├── index.html         # Formulario de reserva, datos de atención y estado del servicio
│   └── styles.css         # Hoja de estilos de la interfaz
├── .env.example           # Plantilla de variables de entorno
├── .gitignore             # Exclusiones de archivos locales y datos sensibles.
├── .semver                # Control de versión
├── Dockerfile             # Definición de imagen basada en nginx:alpine
├── docker-compose.yml     # Orquestación del servicio en el puerto 8080
└── README.md              # Documentación técnica del proyecto