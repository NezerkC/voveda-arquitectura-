---
tipo: hub-relacional
fase: [NUMERO_DE_FASE]
dominio: [NOMBRE_DEL_DOMINIO]
tags:
  - rol/hub
  - dominio/[NOMBRE_DEL_DOMINIO]
  - fase/[NUMERO_DE_FASE]
skills_vinculadas:
  - "[[Nombre de la Skill 1]]"
  - "[[Nombre de la Skill 2]]"
---

# HUB DE [NOMBRE DEL DOMINIO] (BLUEPRINT)

> [!IMPORTANT]
> Este archivo es una plantilla de arquitectura. Úsalo para crear nuevos Hubs Pasivos (Junction Tables) cuando necesites agrupar múltiples skills externas bajo un mismo dominio, evitando acoplar el Orquestador.

## 1. Reglas de Implementación
1. **Archivo 100% Pasivo:** Un Hub jamás debe contener prompts, instrucciones de sistema, ni variables de entorno. Es un registro estático que no consume LLM.
2. **Taxonomía Estricta:** Reemplaza `[NUMERO_DE_FASE]` y `[NOMBRE_DEL_DOMINIO]` en el YAML respetando minúsculas y sin espacios.
3. **Punteros Bidireccionales:** La lista de `skills_vinculadas` usa la sintaxis `[[Nombre del Archivo]]`. Si el archivo de la skill no existe, el Orquestador fallará rápido (Fail-Fast).

## 2. Flujo de Ejecución (Scatter-Gather)
El Orquestador lee los punteros de este archivo e internamente:
1. **Scatter:** Dispara subagentes en paralelo para cada skill listada.
2. **Gather:** Espera a que todas las skills terminen su tarea y consolida el resultado antes de pasar a la siguiente Fase de la Bóveda.
