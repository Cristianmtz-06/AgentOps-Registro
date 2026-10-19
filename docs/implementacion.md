# Implementación del Registro

## Objetivo

Implementar un servicio de Registro utilizando Docker Registry para almacenar y gestionar artefactos dentro de una arquitectura AgentOps.

## Tecnologías Utilizadas

- Windows 11
- Docker Desktop
- Docker Compose
- Docker Registry
- YAML
- GitHub
- Markdown

## Estructura del Proyecto

El proyecto fue organizado siguiendo la estructura recomendada para proyectos de ciencia de datos e inteligencia artificial:

```text
AgentOps-Registro/
│
├── assets/
├── ci-cd/
├── config/
├── deployment/
├── docs/
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

## Archivo docker-compose.yml

```yaml
services:
  registry:
    image: registry:2
    container_name: agentops-registry
    ports:
      - "5000:5000"
    restart: unless-stopped
```

## Despliegue

Para iniciar el servicio se ejecutó el siguiente comando:

```bash
docker compose up -d
```

## Verificación

Se verificó el funcionamiento mediante:

```bash
docker ps
```

Además, se comprobó la disponibilidad del servicio accediendo a:

```text
http://localhost:5000/v2/
```

## Resultado

El contenedor **agentops-registry** se creó y ejecutó correctamente.

El sistema respondió satisfactoriamente mostrando:

```json
{}
```

lo que confirma que Docker Registry se encuentra en funcionamiento y disponible para almacenar artefactos.

## Prueba de Almacenamiento de Artefactos

Para validar el funcionamiento del Registro se realizó una prueba utilizando una imagen Docker de ejemplo.

### Descarga de imagen

```bash
docker pull hello-world
```

### Etiquetado para el Registro

```bash
docker tag hello-world localhost:5000/hello-world:v1
```

### Almacenamiento en el Registro

```bash
docker push localhost:5000/hello-world:v1
```

### Verificación

```bash
curl http://localhost:5000/v2/_catalog
```

### Resultado

El sistema respondió:

```json
{
  "repositories": [
    "hello-world"
  ]
}
```

Esto demuestra que el Registro implementado puede almacenar y administrar artefactos correctamente.

## Conclusiones

La implementación de Docker Registry permitió comprender el funcionamiento del componente Registro dentro de una arquitectura AgentOps.

Las pruebas realizadas demostraron que el sistema puede almacenar y administrar artefactos versionados mediante Docker Compose.

La solución implementada cumple con los requerimientos de contenerización, documentación y gestión de artefactos establecidos para el proyecto.