---
tipo: adr
estado: aceptado
fecha: 2026-09-01
tags:
  - gobernanza/adr
  - arquitectura/escalabilidad
  - patrones/junction-table
  - patrones/scatter-gather
---

# ADR-001: Estrategia de Crecimiento y Escalabilidad de Skills

## 1. Contexto y Problema
A medida que el ecosistema crece incorporando decenas de skills externas, el Grafo Acíclico Dirigido (DAG) corre el riesgo de convertirse en un antipatrón de dependencias tipo "Spaghetti" (N:N). Si un agente de fase intenta conocer todas las skills posibles, el contexto del LLM se desborda, se degrada el razonamiento y se vuelve inmanejable. Además, las tareas monolíticas extensas generan cuellos de botella en la ejecución secuencial.

## 2. Decisión Arquitectónica

Para mantener la Bóveda ordenada y la ejecución rápida, adoptamos tres decisiones fundamentales:

### A. Registros Relacionales Pasivos (Hubs / Junction Tables)
En lugar de conectar skills directamente entre sí o saturar los pilares con agentes activos en el medio, introducimos **Archivos Hub (Registros Pasivos)**.
- **Regla:** Ningún agente de Pilar debe tener una cardinalidad de dependencias Muchos-a-Muchos hardcodeada con skills externas, ni debemos gastar tokens en un "agente mediador" para rutear.
- **Solución:** Se crea un archivo Markdown que actúa como tabla intermedia (Ej: `Hub-Seguridad.md`). Este Hub contiene la metadata relacional. El Orquestador simplemente lee este archivo (rápido y sin costo de inferencia) y, a partir de ahí, invoca directamente en paralelo a las skills específicas.

### B. Taxonomía Estricta de Etiquetas (Tags)
Toda skill nueva debe clasificarse usando namespaces para habilitar el descubrimiento dinámico:
- `fase/{numero}`: Indica el pilar en el que opera.
- `rol/{hub|worker}`: Define si el archivo es un registro de ruteo o una skill ejecutora.
- `dominio/{nombre}`: El contexto limitado (ej. `dominio/seguridad`).

### C. Ejecución Paralela (Patrón Scatter-Gather)
Para evitar bloqueos en tareas de gran volumen:
- **Scatter (Dispersión):** El Orquestador, guiado por el Hub Pasivo, invoca a múltiples subagentes especialistas de manera concurrente, asignándole a cada uno una fracción de la tarea.
- **Gather (Agrupación):** Los subagentes finalizan su trabajo en paralelo y el orquestador consolida los resultados para la siguiente fase.

## 3. Consecuencias (Trade-offs)
- **Positivas:** El DAG se mantiene limpio. No gastamos tokens en agentes mediadores. La velocidad de ejecución baja drásticamente al paralelizar tareas grandes.
- **Negativas:** Requiere disciplina para mantener los archivos Hub (Junction Tables) actualizados cada vez que se agrega una skill nueva a un dominio.
