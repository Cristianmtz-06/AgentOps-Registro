# Investigación: Registro en AgentOps

## Introducción

Dentro de AgentOps, el Registro es un componente encargado de almacenar, administrar y versionar los artefactos utilizados por los agentes inteligentes. Estos artefactos pueden incluir imágenes de contenedores, configuraciones, dependencias, modelos y componentes necesarios para la operación de sistemas basados en inteligencia artificial.

## Importancia del Registro en AgentOps

El Registro permite mantener un repositorio centralizado de artefactos para garantizar la disponibilidad, integridad y reutilización de los componentes utilizados por los agentes.

Entre sus principales beneficios se encuentran:

- Control de versiones.
- Centralización de artefactos.
- Reproducibilidad de despliegues.
- Trazabilidad de componentes.
- Administración organizada de recursos.

## Herramientas Open Source para Registro

### Docker Registry

Docker Registry es una herramienta open source que permite almacenar y distribuir imágenes Docker de forma privada o pública. Es ligera, sencilla de desplegar y ampliamente utilizada en entornos de contenerización.

### Harbor

Harbor es una plataforma empresarial para la gestión de registros de contenedores. Incluye control de acceso, escaneo de vulnerabilidades, firma de imágenes y administración avanzada.

## Comparación de Herramientas

### Docker Registry

**Ventajas**

- Fácil instalación.
- Bajo consumo de recursos.
- Integración nativa con Docker.
- Ideal para proyectos académicos.

**Desventajas**

- Funcionalidad básica.
- Sin interfaz gráfica integrada.

### Harbor

**Ventajas**

- Gestión avanzada de usuarios.
- Escaneo de vulnerabilidades.
- Interfaz web amigable.

**Desventajas**

- Mayor consumo de recursos.
- Implementación más compleja.

## Herramienta Seleccionada

Para el desarrollo de este proyecto se seleccionó **Docker Registry**.

## Justificación

Docker Registry fue seleccionado por ser una solución open source, ligera y fácil de implementar mediante Docker Compose. Además, permite demostrar de manera práctica el concepto de Registro dentro de una arquitectura AgentOps en un entorno aislado.

## Referencias

- https://docs.docker.com
- https://hub.docker.com/_/registry
- https://goharbor.io
- https://yaml.org