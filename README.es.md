# **OAK - Orangecat Ai Kit**

> Crea tus agentes, enlázalos y crea patrones agénticos

![Status](https://img.shields.io/badge/status-design%20phase-orange)

> [!NOTE]
> Este proyecto está en fase de diseño, lo que significa que está siendo diseñado activamente.

## Descripción general

OAK es un kit para desarrollar y conectar agentes, creando patrones agénticos reutilizables.

### Propósito

OAK está diseñado para ser fácil de usar, con una TUI intuitiva con diferentes vistas para administrar tu esquema de agentes.

### Proveedores

Puedes añadir proveedores de IA con un simple plugin o una URL.
Puedes crear tus propios plugins de LLM, por ejemplo, un plugin que ejecuta cada pregunta a la IA a través de un número de iteraciones.

### Ejemplo

Un ejemplo es el patrón **Orquestador-minion**, donde un agente coordinador (`agente orquestador`) delega subtareas a agentes trabajadores especializados (`subagentes`).

## Plan de implementación

**Bloque 3**: Arquitectura — *actual*

- [ ] Escribir el documento de arquitectura (capas, contratos de dominio, interacciones)
  - [ ] Definir las capas arquitectónicas y sus reglas de dependencia
  - [ ] Definir los contratos de dominio de las entidades
  - [ ] Definir los flujos de interacción (Chain/Sub/Super) y el punto de extensión de concurrencia
  - [ ] Definir el modelo de Session y Entry Point
  - [ ] Documentar el contrato de Plugins y los límites de seguridad
  - [ ] Registrar las decisiones abiertas (stack, TUI, almacenamiento) con sus criterios de resolución

## Empezando

Pronto; esta sección será rellenada cuando las tecnologías estén decididas.

## Contribuyendo

Las contribuciones son bienvenidas. Abre un issue o una PR para debatir sobre cambios antes de implementarlos.

## Licencia

Este proyecto está sobre la [licencia MIT](./LICENSE).
