# Portal de Reserva de Horas Médicas — Proyecto DevOps (`unidad1`)

Aplicación web estática desarrollada en HTML5 y CSS3 que simula un portal de reserva de horas médicas para un centro clínico (incluyendo formulario de agendamiento, datos generales de atención y estado del servicio). El servicio está contenerizado sobre **Nginx (`nginx:alpine`)** y preparado para ejecutarse de forma reproducible tanto con **Docker Compose** como mediante comandos directos de **Docker CLI**.

## Requisitos previos

* **Git:** Instalado y configurado en el equipo local.
* **Docker Desktop:** Instalado, iniciado y con el motor de contenedores activo.
* **Navegador web:** Para verificar la interfaz en `http://localhost:8080`.

## Estructura del proyecto

```text
unidad1/
├── src/
│   ├── _static/           # Imagenes utilizadas en formulario
│   ├── index.html         # Formulario de reserva, datos de atención y estado del servicio
│   └── styles.css         # Hoja de estilos de la interfaz web
├── .env.example           # Plantilla de variables de entorno 
├── .gitignore             # Reglas de exclusión para archivos locales y .env
├── .semver                # Control de versión
├── Dockerfile             # Definición de imagen basada en nginx:alpine
├── docker-compose.yml     # Orquestación del servicio y mapeo de puertos
└── README.md              # Documentación técnica del proyecto
```

## Configuración de variables de entorno (`.env`)

El proyecto utiliza variables de entorno para parametrizar el servicio y los puertos sin modificar el código fuente:

1. **Crear el archivo local `.env` a partir de la plantilla:**
   ```bash
   cp .env.example .env
   ```
2. **Parámetros disponibles en `.env`:**
   * `APP_NAME`: Nombre base del servicio (`salud-medica-reservas`).
   * `APP_ENV`: Entorno de ejecución (`local`).
   * `TZ`: Zona horaria del contenedor (`America/Santiago`).
   * `HOST_PORT`: Puerto expuesto en el equipo anfitrión (`8080`).
   * `CONTAINER_PORT`: Puerto interno donde escucha Nginx (`80`).

> **Nota:** El archivo `.env` está excluido en `.gitignore` para evitar publicar configuraciones locales en el repositorio. Si ejecutas el proyecto con Docker Compose sin crear `.env`, se aplicarán por defecto los valores configurados (`8080:80`).

## Instalación y ejecución

Clona el repositorio y accede al directorio del proyecto:

```bash
git clone https://github.com/robirod/unidad1.git
cd unidad1
```


Construye la imagen y levanta el contenedor:

```bash
docker compose up -d
```

## Verificación y monitoreo del servicio

* **Prueba funcional en navegador:** Ingresar a `http://localhost:8080` y comprobar la carga del formulario de reserva de horas, los datos de atención y el estado del servicio.
* **Comandos de verificación con Docker Compose:**
  ```bash
  docker compose ps          # Estado de los servicios levantados
  docker compose logs        # Registros de acceso y errores de Nginx
  ```
* **Comandos de verificación con Docker CLI:**
  ```bash
  docker ps                            # Listar contenedores activos
  docker ps -a                         # Listar todos los contenedores (activos y detenidos)
  docker images                        # Verificar imágenes construidas localmente
  docker logs salud-medica-nginx       # Consultar logs del contenedor
  docker stats --no-stream             # Revisar consumo puntual de CPU y memoria
  ```

## Detención y eliminación (contenedor e imagen)

### Con Docker Compose

* **Detener el contenedor sin eliminarlo** (puede reanudarse con `docker compose start`):
  ```bash
  docker compose stop
  ```
* **Detener y eliminar el contenedor y su red virtual** (conserva la imagen):
  ```bash
  docker compose down
  ```
* **Eliminar el contenedor junto con la imagen construida:**
  ```bash
  docker compose down --rmi all
  ```


## Prácticas de seguridad aplicadas

* No se almacenan credenciales, tokens, claves API ni datos reales de pacientes en el repositorio público.
* Se versiona únicamente `.env.example` como plantilla referencial, bloqueando cualquier archivo `.env` local mediante `.gitignore`.
* Se utiliza la imagen oficial `nginx:alpine` para reducir el tamaño y minimizar paquetes innecesarios.