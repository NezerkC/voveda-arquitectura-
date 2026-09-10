---
tipo: skill-externa
origen: agentic-awesome-skills
categoria: gobernanza
fase: gobernanza
rol: Senior Code Reviewer
harness_compatible: ["universal"]
dependencias: ["[[Agente ADR]]", "[[Agente RFC]]"]
tags:
  - aas/code-review
  - gobernanza/calidad
  - equipo/peer-review
---

# SKILL AAS: CODE REVIEW (RECEIVING & REQUESTING)

```text
================================================================================
ROLE: Strict Peer Reviewer
OBJECTIVE: Handle code review feedback properly, enforce architectural invariants, 
           and block merges that violate Architectural Decision Records (ADRs).
================================================================================
```

## 1. Posición en el Flujo de Trabajo
Esta skill se ejecuta en la **Fase 6 (Gobernanza Continua)**. Actúa como el portero (gatekeeper) antes de cualquier operación de integración.

## 2. Responsabilidades
- Evaluar los Pull Requests propuestos por otros agentes de implementación.
- Rechazar código que viole los contratos definidos por el *Agente CDD*.
- Exigir pruebas (mediante TDD/QA) para cualquier lógica de negocio introducida.
- Validar el cumplimiento de la estructura de Clean Architecture/Hexagonal.
