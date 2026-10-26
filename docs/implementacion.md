# Implementación del Registro en AgentOps

## 1. Objetivo

Implementar y verificar un servicio de Registro utilizando Docker Registry para almacenar y recuperar imágenes de contenedores dentro de una arquitectura AgentOps.

---

## 2. Tecnologías utilizadas

1. Windows 11.
2. Docker Desktop.
3. Docker Compose.
4. Docker Registry.
5. YAML.
6. GitHub.
7. Markdown.

Docker Desktop proporciona el entorno para ejecutar contenedores en Windows. Para cumplir con el requisito de utilizar contenedores sobre un kernel Linux, se debe comprobar que Docker Desktop esté utilizando su backend de Linux.

---

## 3. Estructura del proyecto

El proyecto se organizó siguiendo la estructura recomendada para proyectos de ciencia de datos e inteligencia artificial.

```text
AgentOps-Registro/
├── assets/
├── ci-cd/
├── config/
├── deployment/
├── docs/
│   ├── investigacion.md
│   ├── implementacion.md
│   ├── etica.md
│   └── conclusiones.md
├── frontend/
├── models/
├── monitoring/
├── notebooks/
├── pipelines/
├── scripts/
├── src/
├── tests/
├── README.md
└── docker-compose.yml
```

Las carpetas se pueden ampliar conforme se agreguen nuevas funciones al proyecto.

---

## 4. Configuración del Registro

Se utiliza Docker Registry como servicio para almacenar y distribuir imágenes de contenedores.

El servicio se define mediante un archivo YAML que permite indicar la imagen, el nombre del contenedor, los puertos y las opciones de ejecución.

### 4.1. Archivo `docker-compose.yml`

```yaml
services:
  registry:
    image: registry:2
    container_name: agentops-registry
    ports:
      - "5000:5000"
    restart: unless-stopped
    volumes:
      - registry_data:/var/lib/registry

volumes:
  registry_data:
```

El volumen `registry_data` permite conservar los datos del Registro aunque se elimine o se vuelva a crear el contenedor.

Esta configuración es apropiada para un laboratorio local controlado. No incluye autenticación ni TLS y, por tanto, no debe exponerse directamente a redes no confiables.

---

## 5. Despliegue

Desde la terminal, ubicada en el directorio donde se encuentra el archivo `docker-compose.yml`, se ejecuta:

```bash
docker compose up -d
```

Este comando crea e inicia el servicio en segundo plano.

Para comprobar el estado del contenedor se utiliza:

```bash
docker ps
```

También se puede revisar el estado de los servicios de Compose con:

```bash
docker compose ps
```

---

## 6. Verificación del servicio

Para comprobar la disponibilidad del Registro, se accede a la siguiente dirección desde el equipo local:

```text
http://localhost:5000/v2/
```

También se puede realizar la consulta desde una terminal:

```bash
curl http://localhost:5000/v2/
```

Una respuesta `{}` indica que el endpoint de la API del Registro respondió correctamente.

Para consultar los registros del servicio se puede ejecutar:

```bash
docker compose logs registry
```

---

## 7. Prueba de almacenamiento de imágenes

Para comprobar que el Registro permite almacenar imágenes, se utiliza una imagen de ejemplo.

### 7.1. Obtener una imagen

```bash
docker pull hello-world
```

Este comando necesita conexión a Internet si la imagen no está disponible localmente.

### 7.2. Etiquetar la imagen

```bash
docker tag hello-world localhost:5000/hello-world:v1
```

Este comando asigna un nombre y una etiqueta a la imagen para identificar el repositorio privado.

### 7.3. Publicar la imagen

```bash
docker push localhost:5000/hello-world:v1
```

El comando envía la imagen al Registro local.

### 7.4. Consultar los repositorios

```bash
curl http://localhost:5000/v2/_catalog
```

Una respuesta esperada es:

```json
{
  "repositories": [
    "hello-world"
  ]
}
```

La respuesta anterior es el resultado esperado de la prueba. Debe utilizarse como resultado real únicamente si se obtuvo al ejecutar el comando.

---

## 8. Prueba de recuperación de una imagen

Para comprobar que la imagen puede recuperarse desde el Registro, primero se elimina la etiqueta local:

```bash
docker image rm localhost:5000/hello-world:v1
```

Después se recupera la imagen:

```bash
docker pull localhost:5000/hello-world:v1
```

Si el comando termina correctamente, se habrá comprobado que el Registro permite recuperar la imagen almacenada.

Esta prueba elimina la etiqueta local del repositorio privado, pero no elimina el contenido guardado en el volumen del Registro.

---

## 9. Persistencia de los datos

El volumen `registry_data` permite conservar las imágenes fuera de la capa temporal del contenedor.

Para verificar la persistencia, se puede reiniciar el servicio:

```bash
docker compose restart
```

Después se consulta nuevamente el catálogo:

```bash
curl http://localhost:5000/v2/_catalog
```

Si el repositorio sigue apareciendo, se habrá comprobado que los datos permanecen disponibles después del reinicio.

---

## 10. Preparación para trabajar sin conexión a Internet

Para utilizar el Registro en un ambiente aislado, primero se deben preparar las imágenes necesarias en un equipo con acceso a Internet.

Por ejemplo, para exportar la imagen de Registry:

```bash
docker pull registry:2
docker save -o registry-image.tar registry:2
```

El archivo generado se transfiere al equipo aislado mediante un medio autorizado.

En el equipo aislado se carga la imagen:

```bash
docker load -i registry-image.tar
```

También se deben transferir y cargar las imágenes que se utilizarán para las pruebas, como `hello-world`.

Una vez que las imágenes estén disponibles localmente, se puede iniciar el servicio sin descargarlas de Internet.

**Importante:** no basta con desconectar Internet. Antes deben estar disponibles todas las imágenes y dependencias necesarias para ejecutar el laboratorio.

---

## 11. Seguridad

Para mejorar la seguridad del Registro se recomienda:

1. Restringir el acceso al servicio.
2. Utilizar TLS cuando se permita el acceso desde otros equipos.
3. Configurar autenticación y autorización para ambientes compartidos.
4. Verificar la procedencia y los digests de las imágenes.
5. Mantener las imágenes actualizadas.
6. No incluir credenciales dentro de las imágenes.
7. Realizar copias de seguridad del volumen persistente.

La configuración mostrada utiliza HTTP y no tiene autenticación, por lo que debe limitarse a pruebas locales controladas.

---

## 12. Evidencias de implementación

Para documentar la práctica se recomienda agregar capturas de pantalla de los siguientes elementos:

1. Archivo YAML de configuración.
2. Servicio iniciado correctamente.
3. Salida del comando `docker ps`.
4. Respuesta del endpoint `/v2/`.
5. Publicación de la imagen mediante `docker push`.
6. Consulta del catálogo de repositorios.
7. Recuperación de la imagen mediante `docker pull`.
8. Prueba de persistencia después del reinicio.
9. Operación del servicio con las imágenes preparadas sin conexión a Internet.

Las capturas deben corresponder a las pruebas realmente ejecutadas.

---

## 13. Conclusión

La implementación permite estudiar el funcionamiento de Docker Registry como componente de almacenamiento y distribución de imágenes dentro de AgentOps.

Mediante Docker Compose y YAML se define el servicio, mientras que los comandos de Docker permiten publicar, consultar y recuperar imágenes.

Las pruebas de funcionamiento, persistencia y operación sin conexión permiten comprobar las capacidades del Registro y documentar sus limitaciones.
