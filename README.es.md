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

**Bloque 2**: Fundamento — *actual*

- [x] Definir los conceptos
- [x] Definir los requisitos del proyecto
- [ ] Definir y documentar los axiomas
  - [ ] Definir los criterios de validez de un axioma
  - [ ] Extraer axiomas candidatos de conceptos y requisitos
  - [ ] Validar y reducir a un conjunto mínimo
  - [ ] Documentar los axiomas ([axioms.md](./docs/design/axioms.md))
- [ ] Auditar la consistencia: mapear requisitos y conceptos a sus axiomas fundamentadores
  - [ ] Mapear cada sección de requisitos (§1–§29) a sus axiomas fundamentadores
  - [ ] Revisar [concepts.md](./docs/design/concepts.md) contra los axiomas
  - [ ] Registrar y resolver inconsistencias
- [ ] Derivar los principios de diseño (árbol de derivación)
  - [ ] Derivar Separation of Concerns de los axiomas
  - [ ] Derivar Separation of Responsibilities de los axiomas
  - [ ] Derivar la semántica de interacciones (Chain/Sub/Super) de los axiomas
  - [ ] Documentar el árbol de derivación
- [ ] Definir los no-goals y límites de alcance
  - [ ] Enumerar qué no es OAK (alcance §29)
  - [ ] Documentar los límites de alcance
- [ ] Definir los criterios de salida de la fase de diseño
  - [ ] Definir los criterios de aceptación para cerrar la fase de diseño
  - [ ] Documentar los criterios

## Empezando

Pronto; esta sección será rellenada cuando las tecnologías estén decididas.

## Contribuyendo

Las contribuciones son bienvenidas. Abre un issue o una PR para debatir sobre cambios antes de implementarlos.

## Licencia

Este proyecto está sobre la [licencia MIT](./LICENSE).
