---
tipo: skill-externa
origen: [EJ_AGENTIC_AWESOME_SKILLS]
categoria: [CATEGORIA_ARQUITECTONICA]
usos: [CASO_DE_USO_1, CASO_DE_USO_2]
capacidades: [CAPACIDAD_ESPECIFICA]
rol: [TITULO_DEL_ROL]
harness_compatible: ["universal"]
dependencias_sugeridas: ["[[Agente Requisito 1]]"]
tags:
  - origen/[ORIGEN]
  - uso/[CASO_DE_USO]
  - capacidad/[CAPACIDAD]
---

# SKILL: [NOMBRE DE LA SKILL] (BLUEPRINT)

> [!IMPORTANT]
> Plantilla oficial para registrar nuevas skills en la Bóveda. Copiá este archivo cada vez que descargues una herramienta nueva para integrarla al pipeline del Orquestador.

## 1. Ruteo Dinámico por Casos de Uso (Capacidades)
*   **Enrutamiento por Uso:** Olvidate de las fases secuenciales estrictas. El Orquestador conecta agentes basándose en lo que necesitan resolver. 
*   **Combinación on-the-fly:** Si el Agente de Base de Datos necesita hacer una proyección visual, emitirá un pedido de la capacidad `uso/proyeccion-grafica`. El Orquestador buscará cualquier skill (Ej: Agente Python) que tenga ese tag y armará la combinación dinámicamente.

## 2. System Prompt / Definición
```text
================================================================================
ROLE: [Rol específico del agente]
OBJECTIVE: [Qué debe lograr esta skill de forma medible y estricta]
================================================================================
```

## 3. Responsabilidades y Límites
*   [Definir qué SI hace la skill]
*   [Definir qué NO debe hacer para evitar acoplamiento]
