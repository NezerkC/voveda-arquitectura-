---
tipo: glosario-arquitectonico
patron: metro-ontology
tags:
  - arquitectura/nomenclatura
  - orquestacion/modelos-mentales
  - ddd/ubiquitous-language
---

# ONTOLOGÍA DE ARQUITECTURA: EL MODELO "METRO"

> [!IMPORTANT]
> Para garantizar que tanto humanos como agentes de IA compartan exactamente el mismo modelo mental, adoptamos esta Nomenclatura (Ubiquitous Language basada en Domain-Driven Design) inspirada en una Red de Metro.

## 1. El Diccionario Oficial

| Concepto de Transporte | Concepto Multi-Agente / Bóveda | Descripción Estricta |
| :--- | :--- | :--- |
| **Entrada (Torniquete)** | **Agente Especialista** | Es el punto de acceso. El Agente es la interfaz que recibe el prompt o la tarea y te da "acceso" al trabajo real. |
| **Estación** | **Pilar Arquitectónico** | Es el dominio o contexto limitado (Ej: Pilar Seguridad, Pilar Frontend). Es el lugar físico que agrupa a las entradas (agentes). |
| **Línea de Metro** | **Flujo de Trabajo (Feature / Epic)** | Un caso de uso transversal. Si un requerimiento cruza varios pilares, se traza como una Línea (Ej: La "Línea Login" frena en Frontend, Backend y Base de Datos). |
| **Combinación** | **Hub Simple (Intersección)** | Un punto de cruce donde el flujo salta de un Pilar a otro utilizando solo *algunos* agentes específicos para hacer el pasaje de contexto. |
| **Estación Intermodal** | **Hub Masivo (Scatter-Gather Total)** | Una combinación de alta carga. Ocurre cuando la transición exige despertar a *todos* los agentes del Hub trabajando en paralelo (Swarm completo) para poder continuar el viaje. |

## 2. Impacto en el Agente Orquestador
Bajo esta ontología, el Lead Architect ya no "corre scripts al azar". Cuando entra un requerimiento, el Orquestador:
1. Traza la **Línea** óptima usando Dijkstra.
2. Determina en qué **Estaciones** (Pilares) hay que frenar.
3. Elige qué **Entradas** (Agentes) usar.
4. Evalúa si el peso de la tarea justifica una **Combinación** rápida o si obliga a frenar en una **Intermodal** para procesar todo en paralelo.
