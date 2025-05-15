# Ejemplo de Microservicios con Node.js y Docker

Este proyecto demuestra una arquitectura simple de microservicios utilizando Node.js y Docker. Consta de dos servicios independientes: un **Servicio de Usuarios** y un **Servicio de Productos**, cada uno ejecutándose en su propio contenedor Docker y orquestado con Docker Compose.

## Estructura del Proyecto

```
/microservices-example
  /user-service
    server.js         # Lógica del servicio de usuarios
    package.json      # Dependencias y scripts
    Dockerfile        # Configuración de Docker para el servicio de usuarios
  /product-service
    server.js         # Lógica del servicio de productos
    package.json      # Dependencias y scripts
    Dockerfile        # Configuración de Docker para el servicio de productos
  docker-compose.yml  # Orquesta los servicios
  README.md           # Este archivo
```

## Prerrequisitos

- [Docker](https://www.docker.com/get-started) instalado en tu máquina.
- [Docker Compose](https://docs.docker.com/compose/install/) instalado.

## Instrucciones de Configuración

1. **Clonar o Crear el Proyecto**:
   - Si tienes los archivos del proyecto, asegúrate de que estén organizados como se muestra en la estructura del proyecto arriba.
   - Alternativamente, crea los directorios y copia los archivos proporcionados (`server.js`, `package.json`, `Dockerfile` para cada servicio, y `docker-compose.yml`) en las ubicaciones correspondientes.

2. **Navegar al Directorio del Proyecto**:
   ```bash
   cd microservices-example
   ```

3. **Construir y Ejecutar los Servicios**:
   - Usa Docker Compose para construir y levantar los contenedores:
     ```bash
     docker-compose up --build
     ```
   - Este comando construye las imágenes Docker para ambos servicios y levanta los contenedores.
   - El **Servicio de Usuarios** se ejecutará en `http://localhost:3001`, y el **Servicio de Productos** en `http://localhost:3002`.

## Probar los Servicios

Una vez que los servicios estén en ejecución, puedes probarlos usando un navegador, `curl` o herramientas como Postman.

- **Servicio de Usuarios**:
  - Endpoint: `http://localhost:3001/users`
  - Respuesta esperada:
    ```json
    [
      { "id": 1, "name": "Alice" },
      { "id": 2, "name": "Bob" }
    ]
    ```

- **Servicio de Productos**:
  - Endpoint: `http://localhost:3002/products`
  - Respuesta esperada:
    ```json
    [
      { "id": 1, "name": "Laptop", "price": 999 },
      { "id": 2, "name": "Phone", "price": 499 }
    ]
    ```

Ejemplo usando `curl`:
```bash
curl http://localhost:3001/users
curl http://localhost:3002/products
```

## Detener los Servicios

Para detener los contenedores en ejecución:
- Presiona `Ctrl+C` en la terminal donde se está ejecutando `docker-compose up`, o
- Ejecuta el siguiente comando en el directorio del proyecto:
  ```bash
  docker-compose down
  ```
Esto detendrá y eliminará los contenedores, pero las imágenes permanecerán para uso futuro.

## Notas

- Cada servicio es una aplicación Node.js independiente que utiliza Express, empaquetada en un contenedor Docker.
- El archivo `docker-compose.yml` orquesta los servicios, asignando sus puertos y definiendo sus configuraciones de construcción.
- Este ejemplo es intencionalmente simple, pero puede extenderse con servicios adicionales, bases de datos o comunicación entre servicios.

## Solución de Problemas

- **Conflictos de Puertos**: Asegúrate de que los puertos `3001` y `3002` no estén en uso por otras aplicaciones.
- **Problemas con Docker**: Verifica que Docker y Docker Compose estén instalados y funcionando correctamente.
- **Errores de Construcción**: Confirma que todos los archivos (`server.js`, `package.json`, `Dockerfile`) estén correctamente ubicados y sin errores de sintaxis.

Para más ayuda, consulta la [documentación de Docker](https://docs.docker.com/) o la [documentación de Docker Compose](https://docs.docker.com/compose/).