# Prompmt 1:
Persona: Actúa como el CEO de una empresa de RR. HH. con una dilatada experiencia, principalmente como director de RR. HH., que desea crear una nueva empresa llamada LTI.

Objetivo: Crear una descripción breve de un sistema de seguimiento de candidatos (ATS), incluyendo el valor añadido y la ventaja competitiva, que sirva como documentación base para el proyecto de software del ATS.

# Prompt 2:
Persona: Actúa como el CEO de una empresa de RR. HH. con una dilatada experiencia, principalmente como director de RR. HH., que desea crear una nueva empresa llamada LTI.

Objetivo: Explicar las funciones principales del sistema 

# Prompt 3:
Que persona usarias para crear un prompt efectivo para la creacion de lean canvas sobre el proyecto LTI?

# Prompt 4:
Persona: Actúa como un HR-Tech Venture Architect con experiencia en el lanzamiento de SaaS exitosos para el mercado corporativo. Tu enfoque es el pragmatismo absoluto: buscas la rentabilidad del software resolviendo fricciones operativas reales en el departamento de RR. HH.
Contexto: La empresa se llama LTI. El producto es un ATS (Applicant Tracking System) avanzado. El fundador es un ex-Director de RR. HH. con 20 años de experiencia que está harto de las herramientas burocráticas y lentas que existen actualmente.
Objetivo: Generar un Lean Canvas que valide la viabilidad comercial y operativa de LTI-ATS.
Instrucciones para los bloques clave:

Problema: No menciones "falta de software". Céntrate en la pérdida de talento cualificado, el coste de oportunidad de las vacantes abiertas y la fricción entre RR. HH. y los jefes de departamento.
Propuesta Única de Valor (UVP): Debe ser una declaración que convenza a un CFO (por ahorro) y a un Reclutador (por facilidad de uso).
Ventaja Especial (Unfair Advantage): Utiliza el hecho de que el software está "diseñado por expertos en personas, no solo por programadores".
Canales: Define cómo llegaremos a las grandes empresas sin depender solo de anuncios pagados.
Métricas Clave: Prioriza el Time-to-Fill y el ratio de adopción del sistema por parte de los managers.
Formato: Entrega el Lean Canvas en una tabla Markdown clara y profesional y una imagen en png.

# Prompt 5:
para este mismo proyecto que persona usarias para crear un prompt que genere una descripcion sobre los 3 casos de uso principales con diagramas asociados a ellos.

# Prompt 6:
Persona: Actúa como un Senior Technical Product Manager experto en el desarrollo de plataformas B2B SaaS de automatización (específicamente HR Tech). Eres el puente entre el liderazgo empresarial y el equipo de ingeniería. Tu enfoque es la claridad estructural, la definición de procesos y la viabilidad técnica, siempre referenciando el valor de negocio.

Contexto: La plataforma es LTI-ATS (Applicant Tracking System), referenciando el Lean Canvas de image_0.png. El producto se diferencia por su 'HR Pedigree', su 'Ranking Predictivo' y su enfoque en el 'Hiring Manager'.

Objetivo: Generar la documentación técnica detallada de los 3 casos de uso más críticos y diferenciadores de LTI.

Instrucciones para los Casos de Uso:

Priorización: Los tres casos de uso deben abordar directamente las 'Soluciones' listadas en image_0.png:

UC1: Cribado Inteligente e Identificación de Candidatos Top (Addressing Ranking Predictivo).

UC2: Colaboración Ágil del Hiring Manager (Addressing Interfaz Zero-Training).

UC3: Automatización del Pipeline y Agendación (Addressing Workflows Automatizados).

Estructura de la Descripción: Para cada caso de uso, proporciona:

Nombre: Claro y orientado a la acción.

Actores: Primarios (Reclutador/Manager) y Secundarios (Sistema IA, ERP).

Precondiciones y Gatillo.

Flujo Básico de Eventos: Paso a paso de la interacción.

Valor para el Negocio Referenciado: Conecta el resultado de UC con las métricas de image_0.png (Time-to-Fill, Adopción Manager).

Instrucciones para Diagramas: Para cada caso de uso, describe cómo debe ser el diagrama asociado (por ejemplo, sugiriendo un diagrama de secuencia o un diagrama de flujo de actividad BPMN), detallando qué actores y sistemas deben estar en los carriles (swimlanes) y qué interacciones críticas se deben visualizar. El formato debe ser Mermaid

Formato de Salida: Markdown limpio, estructurado y listo para usar como documentación base en Jira o Notio y un png que replique los diagramas

# Prompt 7
que persona usarias para crear el data model del producto ATS. Debe cubrir entidades, atributos con nombre y tipo y relaciones

# Prompt 8: 
Persona: Actúa como un Senior Data Architect experto en el diseño de bases de datos para plataformas SaaS de alto rendimiento en el sector HR-Tech. Tu enfoque es la normalización (3NF), la integridad referencial y el cumplimiento de normativas de privacidad.

Contexto: La empresa es LTI. El producto es un ATS avanzado que incluye Ranking Predictivo, Portal del Manager y Automatización de Agendas. Necesitamos una estructura de datos que soporte la lógica de negocio definida en el Lean Canvas y los Casos de Uso previos.

Objetivo: Generar el Modelo de Datos (ER Model) que sirva como documentación para el equipo de Backend.

Instrucciones específicas:

Entidades Principales: Incluye al menos: Empresa/Cliente, Vacante/JobPosting, Candidato, Aplicación/Candidatura, Hiring_Manager, Entrevista y Feedback.

Atributos: Para cada entidad, define el nombre del atributo y su tipo de dato (ej. UUID, Varchar, Boolean, Timestamp, JSONB para datos no estructurados de la IA).

Relaciones: Indica claramente la cardinalidad (1:N, N:N) y las claves foráneas (FK).

Lógica de IA: Define cómo se almacenarán los resultados del "Ranking Predictivo" y los datos extraídos del "CV Parsing".

Seguridad: Identifica campos sensibles que requieren cifrado o tratamiento especial.

Formato de salida: Markdown estructurado con tablas para las entidades y una representación textual de las relaciones.

# Prompt 9:
que persona usarias para crear el diseno de alto nivel, tanto explicado como con un diagrama adjunto

# Prompt 10:
Persona: Actúa como un Senior Cloud Solutions Architect con amplia trayectoria en el diseño de plataformas SaaS multitenant. Eres un experto en patrones de diseño, comunicación asíncrona y despliegue en la nube (AWS/Azure/GCP).

Contexto: El proyecto es LTI-ATS. Tenemos definido un Lean Canvas, casos de uso críticos y un modelo de datos relacional. El sistema debe ser altamente escalable y separar la lógica de negocio de los procesos intensivos de IA (Parsing y Matching).

Objetivo: Crear el Diseño de Alto Nivel (HLD) del sistema LTI-ATS.

Instrucciones específicas:

Arquitectura General: Propón una arquitectura (ej. Microservicios o Monolito Modular) justificando la elección.

Componentes Core: Describe las capas de Frontend (Web/Mobile), API Gateway, Servicios de Aplicación y Capa de Datos.

Módulo de IA: Explica cómo se integra el motor de Ranking Predictivo (¿Es un microservicio aparte? ¿Usa colas de mensajería?).

Integraciones Externas: Detalla cómo se gestionan las conexiones con calendarios externos (Google/Outlook) y portales de empleo.

Seguridad y Escalabilidad: Menciona el uso de CDNs, balanceadores de carga y cifrado de datos.

Formato de salida:

Explicación técnica clara en Markdown.

Diagrama de arquitectura utilizando sintaxis Mermaid (tipo graph LR o similar) para visualizar la interacción entre componentes acompanado de un png para visualizarlo

# Prompt 11:
que persona usarias para crea un diagrama C4 de la capa de datos pare ATS?

# Prompt 12:
Persona: Actúa como un Principal Data Architect. Tu especialidad es diseñar infraestructuras de datos para plataformas SaaS de alta concurrencia, asegurando el cumplimiento de GDPR y la eficiencia en costes de almacenamiento.

Contexto: LTI-ATS es un sistema con una base de datos relacional central, pero con necesidades específicas de almacenamiento de archivos (CVs) y caché de sesiones/rankings. Necesitamos bajar al Nivel 2 (Contenedores) y Nivel 3 (Componentes) centrándonos exclusivamente en la persistencia.

Objetivo: Definir el diagrama C4 de la capa de datos de LTI.

Instrucciones específicas:

Nivel 2 (Contenedores de Datos): Identifica y describe los contenedores de persistencia: base de datos transaccional, almacén de objetos, caché y el bus de mensajes (como contenedor de estado temporal).

Nivel 3 (Componentes de Datos): Dentro de la base de datos principal, identifica los esquemas o grupos de tablas lógicas (Tenant Data, Core Recruiting, IA Results).

Flujos de Datos: Describe cómo fluyen los datos entre estos contenedores (ej. sincronización de caché, persistencia de resultados de IA).

Seguridad: Detalla los mecanismos de cifrado en reposo para cada contenedor.

Formato de salida:

Markdown estructurado.

Diagrama Mermaid para el Nivel 2 centrado en persistencia.

Imagen PNG del diagrama