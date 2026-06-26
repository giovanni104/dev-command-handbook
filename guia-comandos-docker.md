# Comandos Básicos de Docker

Guía rápida con los comandos básicos de Docker más utilizados en el día a día por desarrolladores.

Este repositorio sirve como material de consulta para aprender, practicar y recordar comandos esenciales para trabajar con contenedores, imágenes, volúmenes, redes y Docker Compose.

---

## ¿Qué es Docker?

Docker es una plataforma que permite crear, ejecutar y administrar aplicaciones dentro de contenedores.

Un contenedor empaqueta una aplicación junto con sus dependencias, permitiendo que se ejecute de forma similar en diferentes entornos como desarrollo, pruebas o producción.

---

## Verificar instalación

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker --version` | Muestra la versión instalada de Docker | `docker --version` |
| `docker version` | Muestra información detallada del cliente y servidor Docker | `docker version` |
| `docker info` | Muestra información general del entorno Docker | `docker info` |

---

## Imágenes Docker

Las imágenes son plantillas utilizadas para crear contenedores.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker images` | Lista las imágenes descargadas localmente | `docker images` |
| `docker image ls` | Lista las imágenes disponibles | `docker image ls` |
| `docker pull imagen` | Descarga una imagen desde Docker Hub | `docker pull nginx` |
| `docker pull imagen:tag` | Descarga una versión específica de una imagen | `docker pull mysql:8.0` |
| `docker rmi imagen` | Elimina una imagen local | `docker rmi nginx` |
| `docker rmi imagen:tag` | Elimina una imagen específica por versión | `docker rmi mysql:8.0` |

---

## Contenedores Docker

Los contenedores son instancias en ejecución de una imagen.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker ps` | Lista los contenedores en ejecución | `docker ps` |
| `docker ps -a` | Lista todos los contenedores, incluso detenidos | `docker ps -a` |
| `docker run imagen` | Crea y ejecuta un contenedor desde una imagen | `docker run nginx` |
| `docker run -d imagen` | Ejecuta un contenedor en segundo plano | `docker run -d nginx` |
| `docker run --name nombre imagen` | Ejecuta un contenedor con un nombre personalizado | `docker run --name mi-nginx nginx` |
| `docker start contenedor` | Inicia un contenedor detenido | `docker start mi-nginx` |
| `docker stop contenedor` | Detiene un contenedor en ejecución | `docker stop mi-nginx` |
| `docker restart contenedor` | Reinicia un contenedor | `docker restart mi-nginx` |
| `docker rm contenedor` | Elimina un contenedor detenido | `docker rm mi-nginx` |
| `docker rm -f contenedor` | Fuerza la eliminación de un contenedor | `docker rm -f mi-nginx` |

---

## Ejecutar contenedores con puertos

Para acceder a una aplicación dentro de un contenedor desde tu máquina, se deben mapear puertos.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker run -p puertoLocal:puertoContenedor imagen` | Ejecuta un contenedor exponiendo un puerto | `docker run -p 8080:80 nginx` |
| `docker run -d -p puertoLocal:puertoContenedor imagen` | Ejecuta en segundo plano y expone un puerto | `docker run -d -p 8080:80 nginx` |
| `docker run -d --name nombre -p puertoLocal:puertoContenedor imagen` | Ejecuta con nombre, puerto y segundo plano | `docker run -d --name web -p 8080:80 nginx` |

---

## Ejecutar contenedores con variables de entorno

Las variables de entorno permiten configurar aplicaciones dentro del contenedor.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker run -e VARIABLE=valor imagen` | Ejecuta un contenedor con una variable de entorno | `docker run -e MYSQL_ROOT_PASSWORD=123456 mysql:8.0` |
| `docker run --env VARIABLE=valor imagen` | Otra forma de definir variables de entorno | `docker run --env MYSQL_ROOT_PASSWORD=123456 mysql:8.0` |

Ejemplo con MySQL:

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=123456 \
  -e MYSQL_DATABASE=app_db \
  -p 3306:3306 \
  mysql:8.0
```

---

## Logs de contenedores

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker logs contenedor` | Muestra los logs de un contenedor | `docker logs mi-nginx` |
| `docker logs -f contenedor` | Muestra logs en tiempo real | `docker logs -f mi-nginx` |
| `docker logs --tail 100 contenedor` | Muestra las últimas 100 líneas de logs | `docker logs --tail 100 mi-nginx` |

---

## Entrar a un contenedor

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker exec -it contenedor bash` | Entra al contenedor usando bash | `docker exec -it mi-nginx bash` |
| `docker exec -it contenedor sh` | Entra al contenedor usando sh | `docker exec -it mi-nginx sh` |
| `docker exec contenedor comando` | Ejecuta un comando dentro del contenedor | `docker exec mi-nginx ls` |

---

## Inspeccionar contenedores

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker inspect contenedor` | Muestra información detallada del contenedor | `docker inspect mi-nginx` |
| `docker stats` | Muestra uso de CPU, memoria y red de los contenedores | `docker stats` |
| `docker top contenedor` | Muestra procesos ejecutándose dentro del contenedor | `docker top mi-nginx` |

---

## Volúmenes

Los volúmenes permiten persistir información aunque el contenedor sea eliminado.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker volume ls` | Lista los volúmenes existentes | `docker volume ls` |
| `docker volume create nombre` | Crea un volumen | `docker volume create mysql_data` |
| `docker volume inspect nombre` | Muestra detalles de un volumen | `docker volume inspect mysql_data` |
| `docker volume rm nombre` | Elimina un volumen | `docker volume rm mysql_data` |

Ejemplo con volumen en MySQL:

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=123456 \
  -e MYSQL_DATABASE=app_db \
  -p 3306:3306 \
  -v mysql_data:/var/lib/mysql \
  mysql:8.0
```

---

## Redes

Las redes permiten comunicar contenedores entre sí.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker network ls` | Lista las redes Docker | `docker network ls` |
| `docker network create nombre` | Crea una red | `docker network create app-network` |
| `docker network inspect nombre` | Muestra detalles de una red | `docker network inspect app-network` |
| `docker network rm nombre` | Elimina una red | `docker network rm app-network` |

Ejemplo creando una red y usando MySQL:

```bash
docker network create app-network

docker run -d \
  --name mysql-db \
  --network app-network \
  -e MYSQL_ROOT_PASSWORD=123456 \
  -e MYSQL_DATABASE=app_db \
  -p 3306:3306 \
  mysql:8.0
```

---

## Construir imágenes con Dockerfile

Un `Dockerfile` contiene las instrucciones para crear una imagen personalizada.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker build -t nombre-imagen .` | Construye una imagen desde un Dockerfile | `docker build -t mi-app .` |
| `docker build -t nombre-imagen:tag .` | Construye una imagen con versión | `docker build -t mi-app:1.0.0 .` |

Ejemplo básico:

```bash
docker build -t mi-app:1.0.0 .
```

Ejecutar la imagen creada:

```bash
docker run -d --name mi-app -p 8080:8080 mi-app:1.0.0
```

---

## Dockerfile básico para aplicación Java Spring Boot

Ejemplo de `Dockerfile` para una aplicación Spring Boot empaquetada como `.jar`:

```dockerfile
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app

COPY target/app.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

Construir la imagen:

```bash
docker build -t springboot-app:1.0.0 .
```

Ejecutar el contenedor:

```bash
docker run -d --name springboot-app -p 8080:8080 springboot-app:1.0.0
```

---

## Docker Compose

Docker Compose permite definir y ejecutar varios contenedores desde un archivo `docker-compose.yml`.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker compose version` | Muestra la versión de Docker Compose | `docker compose version` |
| `docker compose up` | Levanta los servicios definidos en el compose | `docker compose up` |
| `docker compose up -d` | Levanta los servicios en segundo plano | `docker compose up -d` |
| `docker compose down` | Detiene y elimina los contenedores del compose | `docker compose down` |
| `docker compose ps` | Lista los servicios del compose | `docker compose ps` |
| `docker compose logs` | Muestra logs de los servicios | `docker compose logs` |
| `docker compose logs -f` | Muestra logs en tiempo real | `docker compose logs -f` |
| `docker compose build` | Construye las imágenes definidas en el compose | `docker compose build` |
| `docker compose restart` | Reinicia los servicios | `docker compose restart` |

---

## Ejemplo de docker-compose.yml con MySQL

```yaml
services:
  mysql:
    image: mysql:8.0
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 123456
      MYSQL_DATABASE: app_db
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

Levantar el servicio:

```bash
docker compose up -d
```

Ver contenedores:

```bash
docker compose ps
```

Ver logs:

```bash
docker compose logs -f
```

Detener el servicio:

```bash
docker compose down
```

---

## Limpiar recursos Docker

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `docker system prune` | Elimina recursos no utilizados | `docker system prune` |
| `docker system prune -a` | Elimina imágenes no usadas también | `docker system prune -a` |
| `docker volume prune` | Elimina volúmenes no utilizados | `docker volume prune` |
| `docker network prune` | Elimina redes no utilizadas | `docker network prune` |
| `docker container prune` | Elimina contenedores detenidos | `docker container prune` |
| `docker image prune` | Elimina imágenes sin uso | `docker image prune` |

> **Importante:**  
> Usa los comandos `prune` con cuidado, especialmente si tienes contenedores, imágenes o volúmenes que aún necesitas.

---

## Flujo básico diario con Docker

```bash
docker ps
docker images
docker pull nginx
docker run -d --name web -p 8080:80 nginx
docker logs -f web
docker stop web
docker rm web
```

---

## Flujo básico con Docker Compose

```bash
docker compose up -d
docker compose ps
docker compose logs -f
docker compose down
```

---

## Comandos más usados en el día a día

| Comando | Uso principal |
|---|---|
| `docker ps` | Ver contenedores en ejecución |
| `docker ps -a` | Ver todos los contenedores |
| `docker images` | Ver imágenes locales |
| `docker pull imagen` | Descargar imagen |
| `docker run imagen` | Crear y ejecutar contenedor |
| `docker run -d imagen` | Ejecutar contenedor en segundo plano |
| `docker stop contenedor` | Detener contenedor |
| `docker start contenedor` | Iniciar contenedor |
| `docker restart contenedor` | Reiniciar contenedor |
| `docker rm contenedor` | Eliminar contenedor |
| `docker rmi imagen` | Eliminar imagen |
| `docker logs -f contenedor` | Ver logs en tiempo real |
| `docker exec -it contenedor bash` | Entrar al contenedor |
| `docker build -t nombre .` | Construir imagen |
| `docker compose up -d` | Levantar servicios con Compose |
| `docker compose down` | Detener servicios con Compose |

---

## Recomendaciones

- Usa nombres claros para tus contenedores.
- Usa volúmenes para persistir datos importantes.
- No guardes contraseñas reales directamente en archivos públicos.
- Usa `.env` para manejar variables de entorno.
- Ejecuta `docker ps` para revisar qué contenedores están corriendo.
- Ejecuta `docker logs -f nombre-contenedor` para diagnosticar errores.
- Usa `docker compose` cuando necesites levantar varios servicios.
- Ten cuidado con `docker system prune -a` porque puede eliminar imágenes que luego necesitarás descargar otra vez.

---

## Autor

**Giovanni Hernandez**

Repositorio creado como guía práctica para aprender y consultar comandos básicos de Docker.

---

## Licencia

Este proyecto puede ser utilizado con fines educativos y de práctica.
