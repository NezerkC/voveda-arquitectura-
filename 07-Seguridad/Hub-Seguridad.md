---
tipo: hub-relacional
fase: 4
dominio: seguridad
tags:
  - rol/hub
  - dominio/seguridad
  - fase/4
skills_vinculadas:
  - "[[Skill AAS Security Engineer]]"
  - "[[Agente Zero Trust]]"
  - "[[Agente Sanitizacion Fronteras]]"
---

# HUB DE SEGURIDAD (TABLA INTERMEDIA PASIVA)

```text
================================================================================
ROLE: Junction Table (Declarative Hub)
OBJECTIVE: Map Phase 4 (Security) to its specific executing skills dynamically.
================================================================================
```

Este archivo no es un agente inteligente, es un **registro estático relacional**.

El Orquestador utiliza la propiedad `skills_vinculadas` para saber exactamente a qué agentes especialistas debe disparar en paralelo (patrón Scatter-Gather) cuando entra a la Fase 4 de seguridad.

Al agregar nuevas skills de seguridad de AAS en el futuro, solo se suma el link en este archivo, manteniendo el Grafo principal completamente limpio e intacto.
