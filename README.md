# Evaluacion-2-de-inteligencia-artificial
# Asistente Inteligente de Soporte Técnico IT

**Evaluación Parcial N°2 - Ingeniería de Soluciones con IA (ISY0101)**
**Estudiante:** Nicolás San Martín (Grupo 13)

## Descripción del Proyecto
Este repositorio contiene la implementación de un Agente Inteligente Stateful diseñado para automatizar el Nivel 1 del departamento de Soporte Técnico (IT Helpdesk). El agente interactúa con los empleados, busca soluciones a problemas técnicos y escala los incidentes creando tickets automáticos cuando los pasos iniciales no resuelven el problema.

## Arquitectura y Orquestación
Se seleccionó el framework LangChain por su capacidad para gestionar agentes individuales complejos y su madurez en la integración de herramientas mediante Function Calling[cite: 37].

* **Core Engine (LLM):** API de OpenRouter (modelo `openai/gpt-6-luna`), configurado con `reasoning: low` para optimización de latencia y presupuesto[cite: 37].
* **Planificación:** Patrón ReAct (Reason + Act). El agente piensa, elige una herramienta, observa el resultado y decide su próxima acción de forma iterativa y autónoma[cite: 37].
* **Gestión de Memoria:** Implementación de `ConversationBufferMemory` para mantener el contexto conversacional a lo largo de la sesión. Esto permite al agente recordar el problema original al momento de escalar el incidente, evitando redundancias[cite: 37].

## Herramientas Autónomas (Tools)
El agente utiliza las siguientes herramientas para interactuar con su entorno:
1. `consultar_base_conocimiento`: Integrada con DuckDuckGo Search para recuperar pasos de diagnóstico y posibles soluciones a problemas de hardware, software o conectividad[cite: 37, 38].
2. `crear_ticket_soporte`: Simula la conexión con un sistema para registrar incidentes no resueltos, proporcionando un ID de seguimiento al usuario[cite: 37, 38].

## Instrucciones de Ejecución

### 1. Dependencias
Asegúrese de instalar las versiones exactas para evitar conflictos de compatibilidad:
```bash
pip install -q langchain==0.2.16 langchain-openai==0.1.22 langchain-community==0.2.16 faiss-cpu tiktoken duckduckgo-search
