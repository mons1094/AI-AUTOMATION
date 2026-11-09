
# AI-AUTOMATION - Asistente Virtual con IA para Agencia de Lotería

## Descripción
Este proyecto implementa un asistente virtual inteligente impulsado por Inteligencia Artificial para automatizar la atención al cliente en una agencia de lotería. El sistema procesa consultas y jugadas realizadas a través de WhatsApp, mantiene el contexto de la conversación, gestiona un proceso de aprobación humana (Human-in-the-Loop) y registra automáticamente toda la información en una base de datos en Notion.

## Tecnologías Utilizadas
- n8n: Orquestador de flujos de trabajo y automatización (incluye manejo de errores y triggers).
- Claude (Anthropic): Modelo de IA con capacidades de procesamiento de lenguaje natural y memoria de conversación.
- WATI: Plataforma de mensajería API para la integración y envío de respuestas automatizadas en WhatsApp.
- Notion: Base de datos para el registro y gestión detallada de jugadas.
- Gmail: Sistema de notificaciones para la intervención humana antes del envío del resumen final.

## Beneficios del Sistema
- Optimización del Tiempo: Al delegar la atención y el procesamiento de los mensajes de WhatsApp a la IA, los operadores pueden concentrarse en la atención presencial y telefónica, reduciendo drásticamente los tiempos de espera.
- Precisión Operativa: Registro automático, sin errores humanos, de los datos de cada cliente, números elegidos, tipo de juego y montos.
- Human-in-the-Loop: Control total del proceso mediante un sistema de aprobación final que garantiza que los datos y el resumen se verifiquen antes de comunicarse con el cliente.
- Memoria de Conversación: La IA recuerda el historial de interacciones, permitiendo recolectar datos a lo largo de varios mensajes (nombre, waId, jugadas, etc.) de manera fluida.

## Arquitectura del Flujo
1. Webhook: Recibe el mensaje inicial del cliente desde WhatsApp (número, texto).
2. AI Agent (con Memoria): Procesa el mensaje, entiende el intento del usuario y mantiene el historial de la charla.
3. Manejo Condicional (If Nodes)**: Filtra los datos extraídos por la IA y activa las salidas correspondientes, asegurando que solo se notifique el resumen final.
4. Notion: Almacena de forma estructurada toda la información de la jugada.
5. Gmail (Notificación): Envía un correo electrónico al administrador con el resumen de la jugada generado por la IA para su posterior aprobación.
6. WATI (Sesión): Envía el mensaje final aprobado por el operador al cliente en WhatsApp.
7. Error Trigger: Nodo de manejo de excepciones que notifica cualquier fallo en el flujo vía correo.

## Configuración y Requisitos Previos
Para desplegar este asistente, asegúrate de tener configurado:
- Instancia activa de n8n.
- Cuenta en WATI con el Access Token correspondiente y el Workspace ID integrados en el nodo HTTP Request.
- Base de datos en Notion configurada con las propiedades requeridas.
- Credenciales de API de Anthropic para el motor de IA.
- Configuración de Gmail en n8n para las notificaciones y manejo de errores.
