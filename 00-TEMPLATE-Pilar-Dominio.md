---
tipo: pilar-arquitectonico
dominio: [NOMBRE_DEL_DOMINIO]
tags:
  - pilar/[NOMBRE_DEL_DOMINIO]
---

# PILAR: [NOMBRE DEL PILAR] (Estación Base)

> [!IMPORTANT]
> Plantilla oficial para crear nuevos Pilares (Estaciones) en la Bóveda. Un pilar es una carpeta que funciona como un "Bounded Context" (Contexto Delimitado). Agrupa skills afines y aísla sus responsabilidades para que no contaminen otras áreas.

## 1. Fronteras del Dominio (Bounded Context)
Definí las reglas estrictas de esta estación para evitar el acoplamiento:
*   **Responsabilidad Principal:** [Ej: Manejar toda la capa de persistencia de datos y cachés distribuidas]
*   **Límites (Lo que NO debe hacer):** [Ej: Ningún agente de este pilar debe preocuparse por cómo se ven los datos en el frontend ni por la autenticación HTTP]

## 2. Capacidades Ofrecidas (Catálogo de Usos)
¿Qué sabe hacer este pilar? Enumerá los tags de usos que los agentes de acá le exponen al Orquestador para crear las conexiones dinámicas:
*   `uso/[CAPACIDAD_1]`
*   `uso/[CAPACIDAD_2]`

## 3. Directorio de Skills (Entradas a la Estación)
Listado de los agentes especialistas que trabajan físicamente dentro de esta carpeta:
*   `[Nombre de la Skill 1]`
*   `[Nombre de la Skill 2]`
