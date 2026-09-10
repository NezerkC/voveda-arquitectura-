---
tipo: mapa-rutas
patron: metro-ontology
tags:
  - orquestacion/lineas
  - flujos-de-trabajo
  - sdlc
---

# LÍNEAS DE METRO Y ESTACIONES DE LA BÓVEDA

Este documento define el enrutamiento estándar (Dijkstra Routes) del Agente Orquestador para los casos de uso más comunes en el desarrollo de software.

## 🚇 LÍNEAS DE METRO (Workflows / Epics)

### 1. Línea Roja (Desarrollo End-to-End "Greenfield")
- **Descripción:** Creación de un feature completo desde cero.
- **Ruta Estándar:** `Estación Dominio` ➔ `Estación Contratos` ➔ `Estación Backend` ➔ `Estación Frontend` ➔ `Estación DevOps`.

### 2. Línea Azul (Refactor UI / Frontend Only)
- **Descripción:** Cambios visuales o de experiencia de usuario.
- **Ruta Estándar:** `Estación Frontend` ➔ `Hub Simple: Contratos (Lectura)` ➔ `Estación DevOps`.

### 3. Línea Verde (Hotfix Crítico)
- **Descripción:** Resolución rápida de un bug en producción.
- **Ruta Estándar:** `Estación Observabilidad (Logs)` ➔ `Estación Frameworks (Fix)` ➔ `Estación DevOps`.

---

## 🔄 COMBINACIONES (Hubs Simples - Ruteo Ligero)
*Transiciones donde solo 1 o 2 agentes operan para pasar contexto.*
- **Combinación Contratos-Frontend:** El `Agente OpenAPI` alimenta al `Agente UI/UX`.
- **Combinación Backend-Datos:** El `Agente Hexagonal` define el puerto, el `Agente PostgreSQL` crea el schema.

---

## 🏛️ ESTACIONES INTERMODALES (Hubs Masivos - Scatter Gather)
*Nodos donde ocurre procesamiento en enjambre (Swarm). El workflow se bloquea hasta que todos los subagentes terminen.*

### A. Intermodal de Seguridad (Gatekeeper)
- **Ubicación:** Previo a la Fase DevOps.
- **Agentes Concurrentes:** `Security Engineer`, `Zero Trust`, `Sanitización`.
- **Regla:** Paraleliza escaneos. Si un agente detecta vulnerabilidades, se bloquea el paso a la línea de despliegue.

### B. Intermodal de Gobernanza (Pull Request / Merge)
- **Ubicación:** Fase 6 (Auditoría Continua).
- **Agentes Concurrentes:** `Fitness Functions`, `ADR`, `RFC`, `Code Review`.
- **Regla:** Verifica estáticamente dependencias cíclicas y adherencia a la Clean Architecture.
