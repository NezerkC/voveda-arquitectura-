---
tipo: protocolo-operativo
tags:
  - orquestacion/ingesta
  - triaje
  - dependencias
---

# PROTOCOLO DE INGESTA DE REPOSITORIOS (Triaje)

> [!IMPORTANT]
> Este es el proceso estricto que sigue el Agente Orquestador cuando el usuario solicita revisar un repositorio o dependencia externa. Nunca se instala nada a ciegas en la Bóveda.

## FASE 1: Reconocimiento y Triaje (Solo Lectura)
**Trigger:** El usuario dice *"mira este repo [URL]"*.
1. El Agente escanea el repositorio sin modificar nada.
2. Clasifica el contenido en una de 4 categorías:
   - **Skill (Herramienta individual)**
   - **Paquete de Agentes (Swarm pre-armado)**
   - **Librería (Código puro)**
   - **Servicio (SaaS / API externa)**
3. El Agente emite el diagnóstico y se queda en **Standby** (Pausa) esperando órdenes.

## FASE 2: Sastrería e Instalación (Grill-Me)
**Trigger:** El usuario dice *"instalar skill"* o similar.
1. El Agente activa el modo **Entrevista (Grill-Me)**.
2. Realiza preguntas al usuario para entender:
   - ¿En qué pilar o estación se va a usar?
   - ¿Qué casos de uso (`uso/[capacidad]`) específicos va a cubrir en el proyecto?
   - ¿Qué límites se le van a poner para no acoplarla?
3. Una vez superada la entrevista, el Agente utiliza la plantilla `00-TEMPLATE-Skill-Especialista.md` para generar el archivo de la Skill y la guarda oficialmente en la Bóveda de Arquitectura.
