Proyecto final: Sistema de Gestión de Consultas Institucionales con Inteligencia Artificial

1. Descripción general

El proyecto consiste en el diseño e implementación de un sistema de automatización para gestionar consultas institucionales recibidas por correo electrónico, utilizando herramientas de inteligencia artificial y automatización de procesos.

La solución busca optimizar la recepción, clasificación y respuesta de consultas, reduciendo tareas manuales y facilitando el seguimiento de cada solicitud.

El sistema integra Gmail, Airtable, n8n y OpenAI para construir un flujo de trabajo que permite recibir un correo, registrar la consulta en una base de datos, analizar su contenido mediante inteligencia artificial y generar un borrador de respuesta institucional.

Además, incorpora una instancia de revisión humana antes del eventual envío de la respuesta, con el objetivo de mantener el control sobre las comunicaciones institucionales.

2. Objetivos

Objetivo general

Desarrollar un sistema de automatización con inteligencia artificial que permita gestionar consultas institucionales de manera organizada, eficiente y trazable.

Objetivos específicos

Automatizar la recepción de consultas mediante Gmail.

Registrar la información recibida en una base de datos dinámica en Airtable.

Utilizar inteligencia artificial para interpretar y clasificar las consultas.

Generar resúmenes y propuestas de respuesta institucional.

Actualizar automáticamente los registros con los resultados del procesamiento.

Incorporar una instancia de supervisión y aprobación humana.

Facilitar el seguimiento del estado de cada consulta.

3. Herramientas utilizadas

Herramienta

Función dentro del sistema

Gmail

Recepción de consultas y envío de notificaciones.

Airtable

Registro, almacenamiento y seguimiento de consultas.

n8n

Diseño y ejecución del flujo de automatización.

OpenAI

Interpretación, clasificación y generación de respuestas.

4. Diseño de la base de datos

Se creó una base de Airtable denominada Sistema de Gestión de Consultas IA, compuesta por dos tablas:

Tabla Consultas

Almacena la información correspondiente a cada solicitud recibida. Incluye campos para registrar el contenido de la consulta, correo electrónico, fecha, categoría, resumen, respuesta generada por IA y estado de procesamiento.

Tabla Categorías

Contiene las categorías utilizadas para organizar las consultas:

Académica.

Institucional.

Administrativa.

Otras.

La estructura permite organizar la información y realizar un seguimiento de las solicitudes recibidas.

5. Arquitectura y funcionamiento del flujo

El flujo fue diseñado en n8n mediante la integración de distintos nodos.

Etapa 1. Recepción de consultas

El proceso comienza con un nodo Gmail Trigger, configurado para detectar nuevos correos electrónicos recibidos en una cuenta institucional de prueba.

El disparador recupera información como remitente, asunto y contenido del mensaje.

Etapa 2. Registro en Airtable

Una vez recibido el correo, n8n crea un nuevo registro en la tabla Consultas de Airtable.

De esta manera, cada solicitud queda almacenada para facilitar su consulta y seguimiento posterior.

Etapa 3. Procesamiento mediante inteligencia artificial

El contenido del correo se envía a un modelo de OpenAI, al que se le proporciona una instrucción específica para:

Identificar la categoría de la consulta.

Elaborar un resumen de la solicitud.

Redactar una propuesta de respuesta institucional.

Evitar inventar información que no se encuentre disponible.

La respuesta generada se utiliza como borrador para su posterior revisión.

Etapa 4. Actualización de la base de datos

El resultado del procesamiento se incorpora al registro correspondiente de Airtable mediante un nodo de actualización.

También se actualiza el estado de la consulta para identificar que fue procesada por inteligencia artificial y que requiere aprobación.

Etapa 5. Supervisión humana

El sistema envía una notificación por Gmail informando que existe una consulta procesada y un borrador pendiente de revisión.

Posteriormente, el flujo utiliza un nodo Wait para pausar su ejecución y permitir una instancia de intervención humana.

Se incorporó además un nodo IF para evaluar la decisión de aprobación o rechazo.

La lógica de las ramas de aprobación y rechazo quedó incorporada en el diseño, aunque su funcionamiento completo requiere ajustes y validaciones adicionales.

6. Supervisión humana y responsabilidad institucional

Uno de los criterios centrales del proyecto es que la inteligencia artificial no sustituya la intervención humana en las comunicaciones institucionales.

La IA funciona como herramienta de asistencia: interpreta el contenido, organiza la información y propone una respuesta.

La revisión humana permite verificar la pertinencia, exactitud y adecuación institucional del texto antes de enviarlo al destinatario.

Este mecanismo busca reducir el riesgo de respuestas incorrectas, información inventada o comunicaciones que no se ajusten a los criterios de la institución.

7. Pruebas realizadas

Durante el desarrollo se realizaron pruebas utilizando una cuenta de Gmail de prueba y consultas ficticias.

Se verificaron los siguientes componentes:

Detección de nuevos correos mediante Gmail Trigger.

Creación de registros en Airtable.

Procesamiento de consultas mediante OpenAI.

Generación de categorías, resúmenes y borradores de respuesta.

Actualización de registros en Airtable.

Envío de notificaciones por Gmail.

Pausa y reanudación del flujo mediante Wait.

La evaluación de las ramas de aprobación y rechazo del nodo IF quedó pendiente de validación definitiva.

8. Seguridad y control

Para el desarrollo se utilizaron cuentas y datos de prueba.

Las credenciales de acceso a los servicios se administran mediante las credenciales configuradas en n8n. No deben exponerse claves API, contraseñas ni información sensible en capturas, documentación o videos de demostración.

Asimismo, se considera necesario verificar la información generada por IA antes de utilizarla como respuesta institucional definitiva.

9. Conclusiones

El proyecto permitió construir un flujo de automatización que integra herramientas de gestión de información, inteligencia artificial y correo electrónico.

La solución demuestra cómo es posible automatizar distintas etapas de un proceso administrativo, desde la recepción de una consulta hasta su análisis y preparación de una respuesta.

La incorporación de una instancia de supervisión humana constituye un elemento fundamental para asegurar que la automatización se utilice de manera responsable.

Como etapa de mejora, se propone completar la validación de las decisiones de aprobación y rechazo, estructurar los resultados de IA en campos independientes y ampliar las pruebas con diferentes tipos de consultas.

En conjunto, el desarrollo constituye una primera implementación funcional de un sistema de gestión de consultas asistido por inteligencia artificial.
