# AgentOps - Registro

## Autor

Cristian Eduardo de Luna Martínez

## Descripción

Implementación del componente Registro dentro de una arquitectura AgentOps utilizando Docker Registry.

## Objetivo

Implementar un Registro funcional mediante Docker Compose y Docker Registry para el almacenamiento y administración de artefactos.

## Tecnologías Utilizadas

- Docker Desktop
- Docker Compose
- Docker Registry
- YAML
- GitHub
- Markdown

## Ejecución

```bash
docker compose up -d
```

## Verificación

```bash
docker ps
```

## Acceso

http://localhost:5000/v2/

## Estado Actual

- Docker Registry desplegado.
- Prueba de almacenamiento de artefactos completada.
- Documentación creada.
- Evidencias obtenidas.


## Arquitectura

```text
                AgentOps

                     │

                     ▼

          Docker Registry

                     │

      ┌──────────────┼──────────────┐

      ▼              ▼              ▼

 hello-world:v1   agente:v1    modelo:v1
```