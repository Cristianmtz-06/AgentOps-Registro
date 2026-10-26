# Conclusiones

## 1. Conclusión general

El desarrollo del proyecto AgentOps-Registro me permitió estudiar la importancia del Registro dentro de una arquitectura AgentOps y su función en el almacenamiento, organización y distribución de imágenes de contenedores.

La investigación de Docker Registry y Harbor permitió identificar dos alternativas de código abierto con diferentes niveles de complejidad. Docker Registry se seleccionó para la propuesta debido a su configuración sencilla y su compatibilidad con Docker Compose.

---

## 2. Aprendizajes obtenidos

Durante el desarrollo del proyecto se abordaron los siguientes aspectos:

1. La función de un Registro dentro de AgentOps.
2. El uso de herramientas de código abierto para administrar imágenes.
3. La configuración de servicios mediante archivos YAML.
4. El despliegue de contenedores utilizando Docker Compose.
5. La publicación y recuperación de imágenes mediante comandos de Docker.
6. La importancia del almacenamiento persistente.
7. Las medidas de seguridad necesarias para proteger un registro privado.
8. Los requisitos para utilizar imágenes de contenedores en ambientes aislados.

---

## 3. Cumplimiento de los objetivos

El proyecto se orientó a investigar una herramienta de Registro, justificar su selección y proponer una implementación mediante tecnologías de contenerización.

El cumplimiento práctico debe respaldarse con las pruebas ejecutadas, los resultados obtenidos y las evidencias correspondientes.

La documentación en Markdown y la organización del repositorio de GitHub permiten presentar la investigación y los procedimientos de manera estructurada.

---

## 4. Limitaciones y mejoras futuras

Como mejoras futuras se propone:

1. Configurar autenticación y TLS.
2. Incorporar herramientas de análisis de vulnerabilidades.
3. Implementar copias de seguridad del almacenamiento persistente.
4. Documentar los digests de las imágenes utilizadas.
5. Automatizar las pruebas mediante scripts.
6. Evaluar Harbor si se requieren funciones avanzadas de administración.
7. Comprobar el funcionamiento completo del laboratorio sin conexión a Internet.

---

## 5. Conclusión final

El Registro constituye un componente importante para administrar los artefactos utilizados por los agentes inteligentes, ya que facilita su almacenamiento, distribución y recuperación.

Docker Registry ofrece una alternativa adecuada para estudiar estas funciones en un laboratorio académico. Sin embargo, su utilización debe complementarse con medidas de seguridad, mantenimiento, documentación y validación de resultados.

La experiencia permite comprender cómo las tecnologías de contenerización pueden contribuir a organizar los componentes de una arquitectura AgentOps y cómo una implementación debe acompañarse de pruebas y evidencias que demuestren su funcionamiento.
