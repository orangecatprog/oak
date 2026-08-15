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

## Stack tecnológico

- **Lenguaje**: Go — el Core, el Kernel y la TUI.
- **TUI**: Charm (Bubble Tea, Lip Gloss, Bubbles), como adaptador Externo sobre los puertos del Core.
- Consulta [docs/design/tech-stack.md](./docs/design/tech-stack.md) para la decisión y sus criterios.

## Empezando

Pronto; la implementación comienza en el Bloque 5.

## Contribuyendo

Las contribuciones son bienvenidas. Abre un issue o una PR para debatir sobre cambios antes de implementarlos.

## Licencia

Este proyecto está sobre la [licencia MIT](./LICENSE).
