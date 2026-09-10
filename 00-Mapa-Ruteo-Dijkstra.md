---
tipo: mapa-conceptual
patron: dijkstra-routing
tags:
  - arquitectura/ruteo-dinamico
  - orquestacion/grafos
---

# MAPA CONCEPTUAL: RUTEO DINÁMICO CON HUBS TRANSICIONALES (DIJKSTRA)

En lugar de un pipeline secuencial estricto, la Bóveda opera como un grafo ponderado. Los **Hubs** ya no solo agrupan skills estáticas dentro de una fase, sino que actúan como "Peajes" o "Gateways" de transición entre los Pilares. 

Cada transición tiene un "Costo" algorítmico (basado en consumo de tokens, tiempo de ejecución de las skills y riesgo de la operación). El Agente Orquestador utiliza lógica de caminos mínimos (Algoritmo de Dijkstra) para decidir la ruta más eficiente para llevar un requerimiento a producción, esquivando pilares innecesarios.

## Grafo de Transición de Estados

```mermaid
graph TD
    classDef pilar fill:#2c3e50,stroke:#34495e,stroke-width:2px,color:#fff,shape:circle;
    classDef hub fill:#e67e22,stroke:#d35400,stroke-width:2px,color:#fff,shape:hexagon;

    %% Pilares (Nodos de Estado Canónicos)
    P1(((1. Dominio))):::pilar
    P2(((2. Contratos))):::pilar
    P3(((3. Arquitectura))):::pilar
    P4(((4. Resiliencia & Seguridad))):::pilar
    P5(((5. Observabilidad))):::pilar
    P6(((6. DevOps & Infra))):::pilar
    P7(((7. Frontend))):::pilar

    %% Hubs Transicionales (Gateways de ruteo)
    H1_2{Hub: Modelado API}:::hub
    H2_3{Hub: Código Backend}:::hub
    H2_7{Hub: Tokens Visuales}:::hub
    H3_4{Hub: Hardening & Fault Tolerance}:::hub
    H4_5{Hub: Telemetría OTel}:::hub
    H5_6{Hub: Despliegue CI/CD}:::hub
    H7_6{Hub: Empaquetado Web}:::hub

    %% Rutas y Pesos (Dijkstra Cost)
    P1 -- "Costo: Alto (20)" --> H1_2 --> P2
    P2 -- "Costo: Medio (15)" --> H2_3 --> P3
    P2 -- "Costo: Bajo (5)"  --> H2_7 --> P7
    
    P3 -- "Costo: Alto (20)" --> H3_4 --> P4
    P4 -- "Costo: Medio (10)" --> H4_5 --> P5
    P5 -- "Costo: Bajo (5)" --> H5_6 --> P6
    P7 -- "Costo: Medio (10)" --> H7_6 --> P6
```

## ¿Cómo funciona el cálculo de Dijkstra en este flujo?

Si el sistema recibe un requerimiento, el Orquestador evalúa los pesos del grafo:

**Escenario A: "Agregar un nuevo módulo de pagos"**
* Requiere Dominio (P1) -> Contratos (P2) -> Arquitectura (P3) -> Seguridad & Resiliencia (P4) -> Observabilidad (P5) -> DevOps (P6).
* **Costo Total:** 20 + 15 + 20 + 10 + 5 = **70**. Ruta integral de producción, se despliegan los especialistas de backend y hardening.

**Escenario B: "Cambiar el color del botón principal y tipografía"**
* El Orquestador detecta que no hay mutación de datos ni backend. El costo de pasar por P1, P3, P4 y P5 es innecesario.
* Entra por Contratos UI (P2) -> Hub Tokens Visuales (Costo 5) -> Frontend (P7) -> Hub Empaquetado Web (Costo 10) -> DevOps (P6).
* **Costo Total:** 5 + 10 = **15**. 
* **Resultado:** El sistema toma el atajo (shortest path). Se ahorra el tiempo y los tokens de despertar a los agentes de persistencia y seguridad profunda.
