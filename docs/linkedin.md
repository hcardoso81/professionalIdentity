# LinkedIn - Diagnostico y cambios propuestos

Relevamiento del perfil https://www.linkedin.com/in/cardosohernan/ realizado el 14 de octubre de 2026, comparado contra el CV y la documentacion de este repositorio.

Los textos para pegar estan en ingles porque el perfil apunta a roles remotos internacionales y el headline y la experiencia mas reciente ya estan en ingles. Las versiones en espanol estan en [cv-hernan-cardoso-es.html](../cv-hernan-cardoso-es.html).

## 0. Avance (14 de octubre de 2026, segunda lectura del perfil)

El perfil publicado es la fuente de verdad. El CV y la documentacion ya se alinearon con estos datos.

Aplicado en LinkedIn:

| Item | Publicado |
|---|---|
| 404 Crafters | Senior Full Stack Engineer · nov. 2023 - actualidad · descripcion nueva |
| Insider Latam | Full Stack & AI Automation Developer · autonomo · oct. 2024 - actualidad |
| Mundialito Senior | Full Stack & AI Developer · independiente · mar. 2026 - jul. 2026 · pendiente de implementacion del lado del cliente |
| IntermarketFlow | WordPress Plugin Developer · independiente · ago. 2025 - actualidad |
| Aptitudes | 43 en total. Se agregaron TypeScript, Material-UI, GitHub Actions, Google Gemini, Google Apps Script, IA generativa, Modelos de Lenguaje de Gran Tamano (LLM), Arquitectura de software, API de OpenAI, NestJS, Twilio, MailChimp y Seguridad de aplicaciones web. Se quitaron AngularJS, SQL Server y las duplicadas de Web Services. |

Aplicado en la tercera lectura (mismo dia):

- **Acerca de**: publicado, con aptitudes principales TypeScript, React.js, WordPress, Arquitectura de software y LLM.
- **Doppler**: Senior WordPress Developer / Scrum Master, descripcion nueva en ingles.

Estado del CV: **sincronizado con LinkedIn** (titulos, fechas, descripciones, aptitudes principales, educacion e idioma). Si cambias algo en LinkedIn, avisame y actualizo el CV.

Mejoras opcionales que siguen abiertas en LinkedIn (no generan inconsistencias con el CV):

- **Crecimiento profesional**: fechas (mar. 2023 - oct. 2023) y descripcion nueva aplicadas.
- **Intercomgi y Avatar**: descripciones en espanol con errores de tipeo.
- **Proyectos y Destacado**: vacios. El CV tiene 4 tarjetas de proyectos para replicar y el CV online sirve para Destacado.
- **Ingles**: Competencia basica profesional; revisar si refleja tu nivel actual.
- **Aptitudes viejas**: AngularJS, Microsoft SQL Server, SQL Server, Servicios web, Web Services e Infraestructura de software.

Cobertura del perfil frente a busquedas tipicas de recruiters: ver [busquedas-recruiters.md](busquedas-recruiters.md).

Criterios acordados en la revision (aplican tambien a las secciones de abajo):

- No publicar el resultado de la validacion de Insider (20 casos) ni otras metricas internas del cliente.
- Menos detalle interno (cantidad de tests, SHA-256, HMAC, cantidad de commits) y mas responsabilidades y resultados.
- Mundialito Senior se presenta como desarrollo para un cliente, presentado y pendiente de implementacion; no como sistema en produccion.
- No inferir fechas de empleo a partir de commits.

## 1. Estado inicial (primera lectura)

| Seccion | Estado hoy | Prioridad |
|---|---|---|
| Headline | `Senior Full Stack & Applied AI Engineer \| React, TypeScript & LLM Applications`. Bien orientado. | Baja |
| Banner y foto | Banner con el mismo mensaje del headline. Bien. | - |
| Acerca de | **No existe.** Es lo primero que lee un reclutador y donde LinkedIn muestra las 5 aptitudes principales. | **Critica** |
| Destacado | No existe. | Alta |
| Experiencia | 5 entradas. Faltan Insider Latam, IntermarketFlow y Mundialito Senior: casi todo el trabajo de IA de 2026 no aparece. La de 404 Crafters describe solo un proyecto y tiene un titulo generico. | **Critica** |
| Proyectos | Vacia. | Alta |
| Aptitudes (30) | Falta **TypeScript**, ademas de IA, Docker, AWS y arquitectura. Hay duplicados y tecnologias obsoletas. Varias aptitudes estan asociadas a la experiencia equivocada. | Alta |
| Idiomas | Ingles como "Competencia basica profesional", por debajo de lo que dice el CV. | Media |
| Educacion | Ingenieria en Sistemas y Analista Programador (UNICEN). Correcta. | - |
| Recomendaciones | 10, muy buenas y consistentes. La mas reciente sobre trabajo tecnico es de 2025 y ninguna menciona IA. | Media |
| Aplicaciones vinculadas | Gamma, IntelliJ IDEA, HubSpot y Replit Agent. Ninguna refleja tu stack real. | Baja |
| Actividad | La ultima publicacion propia es un juego (Zip). No hay publicaciones sobre tus proyectos. | Media |

### Inconsistencias con el CV

| Dato | LinkedIn | CV | Propuesta |
|---|---|---|---|
| Inicio en 404 Crafters | dic. 2023 | nov. 2023 | Usar **dic. 2023** en ambos: los commits empiezan en diciembre. Confirmar. |
| Titulo en 404 Crafters | Ingeniero de software | Senior Frontend / Full Stack Engineer | **Senior Full Stack Engineer** |
| Periodo de crecimiento profesional | mar. 2023 - jun. 2024 | feb. 2023 - nov. 2023 | **mar. 2023 - nov. 2023**. Hoy se superpone 7 meses con 404 Crafters. |
| Ingles | Basica profesional | Upper-Intermediate | **Competencia profesional** (ver seccion 6) |

## 2. Acerca de (seccion nueva)

Limite: 2.600 caracteres. Este texto tiene unos 2.000.

```text
I'm a Senior Full Stack Engineer with 18+ years building and modernizing production web applications. Today I work mostly with React and TypeScript on complex administrative platforms, and I design applied AI systems that solve real operational problems.

What I'm working on:
• Portal Expensas (404 Crafters): a condominium management platform built with React, TypeScript, Apollo GraphQL and Material UI. Clean Architecture + CQRS + Presenter Pattern, realtime support tickets over GraphQL subscriptions, and a delivery pipeline with GitHub Actions, Docker and AWS.
• Insider Automation: an AI editorial pipeline that turns press releases received by email into WordPress drafts for human review, built on Google Apps Script and the Gemini API. Editors stay in control of every publication.
• A WhatsApp AI assistant built for an amateur football tournament organizer: NestJS, OpenAI function calling with seven tools, live data with fallback and answer checks against real data.

How I work:
• Validate ideas with low-cost POCs, then re-architect deliberately once they prove their value.
• Keep business logic separate from UI and infrastructure, so products can change without rewrites.
• Use AI coding agents (Claude Code, Codex) with explicit rules, ADRs and tests: speed without losing control.
• Communicate clearly with clients and non-technical teams. I've led teams and worked as Scrum Master.

Background: ten years as the WordPress and PHP reference at Doppler, and earlier project lead for brands like Mastercard, Greenpeace and Coca-Cola. That experience with legacy systems is now a strength when modernizing them.

Stack: React · TypeScript · Node.js · NestJS · GraphQL · PostgreSQL · Gemini and OpenAI APIs · Google Apps Script · Docker · GitHub Actions · AWS · WordPress/PHP

Based in Tandil, Argentina. Working remotely with international teams.
```

Aptitudes principales (las 5 que se fijan en el Acerca de):

1. React.js
2. TypeScript
3. Node.js
4. Large Language Models (LLM)
5. Software Architecture (Arquitectura de software)

## 3. Experiencia

Limite por descripcion: 2.000 caracteres. Antes de editar, desactiva **"Compartir actualizaciones del perfil con tu red"** en el formulario. Asi tus contactos no reciben una notificacion por cada cambio. Dejala activa solo si queres anunciar una posicion nueva.

### 3.1 404 Crafters (publicado)

- Titulo: **Senior Full Stack Engineer**
- Tipo de empleo: Jornada completa · En remoto
- Fechas: nov. 2023 - actualidad

```text
Develop and maintain production web applications for international clients, with a focus on React, TypeScript, and complex business workflows.

• Portal Expensas: build a condominium management platform covering settlements, payroll, payments, units, suppliers, and documents. Develop interfaces and business workflows using React, TypeScript, Material UI, and Apollo GraphQL, applying Clean Architecture, CQRS, and the Presenter Pattern.
• Portal de Aliados – Fanki: developed a B2B portal for event operations, sales, payments, attendance, and business metrics. Built dashboards, exportable reports, and interfaces with role-based access using React, TypeScript, and Material UI.
• News Kiosk: contributed across the frontend and backend of a news analysis platform for a US client. Developed search interfaces, dashboards, saved searches, PDF viewing, and email-sharing features using React, React Query, Node.js, Express, and MongoDB.
• Configure AWS environments and CI/CD workflows with GitHub Actions, Docker, and Docker Compose to support application delivery and deployment.

Collaborate directly with clients and teammates in English to clarify requirements, discuss technical decisions, and deliver maintainable solutions.
```

### 3.2 Insider Latam (publicado)

- Titulo: **Full Stack & AI Automation Developer**
- Tipo de empleo: Autonomo · En remoto
- Fechas: oct. 2024 - actualidad

```text
Develop and maintain insiderlatam.com, a Latin American news portal, as an independent developer supporting editorial and marketing workflows.

• Build an AI editorial pipeline that transforms press releases received by email into WordPress drafts for human review, using Google Apps Script and the Gemini API. Integrate content processing, editorial instructions, and WordPress draft creation while keeping editors in control of publication.
• Develop custom WordPress plugins and integrations, including a responsive newsletter builder, editorial filters, a YouTube Shorts carousel, and sports and event coverage widgets.
• Extend WordPress functionality with PHP, JavaScript, external APIs, and custom administrative tools tailored to the editorial team's needs.
• Maintain and modernize the site through PHP upgrades, plugin updates, troubleshooting, and performance improvements.

Work directly with the client to clarify requirements, evaluate practical solutions, and support ongoing site operations.
```

### 3.3 Mundialito Senior (publicado)

- Titulo: **Full Stack & AI Developer**
- Tipo de empleo: Profesional independiente · En remoto
- Fechas: mar. 2026 - jul. 2026

```text
Developed a WhatsApp AI assistant for a client running amateur football tournaments, allowing participants and organizers to ask about fixtures, results, standings, teams, and tournament rules in natural language.

• Built the backend with NestJS, TypeScript, PostgreSQL, and Twilio, integrating OpenAI function calling with seven tools to retrieve tournament information.
• Connected the assistant to the CopaFacil API and a Google Docs FAQ to answer questions using external data and tournament documentation.
• Implemented request signature validation, retries, API fallbacks, and response checks against tool results to reduce unsupported answers.
• Developed administrative tools for tournament configuration, data synchronization, and conversation review, plus a testing environment using the same processing pipeline.

Demonstrated the solution to the client and received positive feedback. The project has not launched; implementation remains pending on the client's side.
```

### 3.4 IntermarketFlow (publicado)

- Titulo: **WordPress Plugin Developer**
- Tipo de empleo: Profesional independiente · En remoto
- Fechas: ago. 2025 - actualidad

```text
Develop and maintain SEO Content Locker, a custom WordPress plugin for premium content access and lead capture on intermarketflow.com, a financial markets analysis website.

• Implement email-based content access with trial expiration and session restoration.
• Build layered anti-bot protection using reCAPTCHA v3 and rate limiting by IP address, form, and email.
• Integrate Mailchimp with dynamic tags and lead-source tracking to support marketing workflows.
• Develop administrative tools for lead management, CSV exports, and daily lead reports scheduled through WP-Cron.
• Refactor procedural code into modular PHP services, repositories, and an event-based notification system to improve maintainability.

Work directly with the client to refine requirements, troubleshoot issues, and deliver ongoing improvements.
```

### 3.5 Crecimiento profesional (publicado)

- Titulo: Crecimiento profesional · Descanso profesional
- Fechas: mar. 2023 - oct. 2023

```text
Planned career break focused on expanding my full stack skills, with an emphasis on React, TypeScript, Node.js, and React Native.

• Self-directed learning in React, Node.js, and React Native, alongside Laravel 10 (Livewire, Eloquent, Sanctum) and WordPress/WooCommerce customization using hooks and filters.

• Collaborated with a small team on CUTI, a mobile app for voice calls and recordings between companies and investors. The app used React Native and Node.js with TypeScript, a REST API, Agora for calls, and Amazon S3 for recording storage. My contributions included login and registration flows.

• Started a structured English program in April 2023, attending two classes per week, and completed it in 2026 to support collaboration with international teams.
```

### 3.6 Doppler (editar)

- Titulo: **Senior WordPress Developer / Scrum Master**
- Aptitudes asociadas: WordPress, PHP, MySQL, JavaScript, Scrum (sacar Socket.io, Mongoose y Express.js de esta experiencia)

La descripcion actual esta en espanol, menciona "ingles B1", "actualmente trabajo en Laravel 7" y Drupal. Reemplazala por:

```text
Technical owner of Doppler's institutional WordPress websites for ten years.

• Maintained and evolved 5 WordPress sites (fromdoppler.com, doppleracademy.com, goemms.com and others) for marketing, internal requests and integrations.
• Integrated external APIs such as Twitter, Zoho and GoToWebinar.
• Supported GOEMMS, one of the largest marketing events in Latin America, across 5 editions: high-traffic website, live streaming and a cached Twitter API integration.
• Owned deployments, NGINX configuration, hosting migrations, performance and SEO.
• Technical reference for other teams when researching, prioritizing and designing new functionality.
```

### 3.7 Intercomgi (editar)

```text
Scrum Master and frontend developer for a JavaScript single-page web application.
```

Sacar la mencion a Backbone.js y la aptitud AngularJS.

### 3.8 Avatar (editar)

Corregir errores de tipeo ("Lationamérica", "latino américa") y llevar el texto al ingles:

```text
Project lead, Scrum Master and senior PHP developer for major Latin American clients.

• Led the development and maintenance of websites for Greenpeace Latin America, Mastercard, Banco Nacion Argentina, Fashion TV Project Runway, Disney Highway Zapping Zone, a Coca-Cola extranet, Sherwin Williams and Telcosur.
• Coordinated development teams and owned the quality of delivered products.
```

## 4. Proyectos (seccion nueva)

Agregalos desde **Anadir seccion > Recomendado > Proyectos** y asocia cada uno a su experiencia.

| Proyecto | Asociado a | Fechas |
|---|---|---|
| Insider Automation - Editorial AI Pipeline | Insider Latam | may. 2026 - actualidad |
| WhatsApp AI Tournament Assistant | Mundialito Senior | mar. 2026 - jul. 2026 |
| Portal Expensas Admins | 404 Crafters | may. 2025 - actualidad |
| SEO Content Locker | IntermarketFlow | 2024 - actualidad |

Textos:

```text
Insider Automation - Editorial AI Pipeline
AI pipeline that turns press releases received by Gmail, with attachments, Google Docs, images and videos, into WordPress drafts for human review. Google Apps Script + Gemini API, resumable batches that work around platform execution limits, idempotent attempts, prompts editable without deploys, multi-source featured-image selection, house-style validation and a WordPress control panel. Built on documented ADRs and a local test suite with Google service doubles.
```

```text
WhatsApp AI Tournament Assistant
WhatsApp assistant for amateur football tournaments built with NestJS, Twilio, OpenAI, PostgreSQL, Google Docs and the CopaFacil API. Multi-tournament sessions, seven strict function-calling tools, live data with fallback, and a hallucination guard that degrades to a safe answer when a response is not grounded.
```

```text
Portal Expensas Admins
Administrative platform for condominium management built with React, TypeScript, Vite, Material UI, MUI X DataGrid and Apollo GraphQL. Clean Architecture, CQRS and Presenter Pattern, realtime tickets over GraphQL subscriptions, several portals compiled from one shared core, and deployment with GitHub Actions, Docker, GHCR and AWS Lightsail.
```

```text
SEO Content Locker
Custom WordPress plugin for premium content access and lead capture: email-based access with trial expiration, reCAPTCHA v3 and rate limiting, Mailchimp sync, admin lead management, CSV export and a daily WP-Cron report. Modular PHP with services, repositories and an event-based notifier.
```

## 5. Aptitudes

Hoy tenes 30. La propuesta deja unas 40, ordenadas por relevancia. LinkedIn conserva las validaciones de las aptitudes que no borres.

### Quitar (duplicadas, obsoletas o poco relevantes)

| Aptitud | Motivo |
|---|---|
| AngularJS | Obsoleta; no forma parte de tu experiencia actual. |
| Microsoft SQL Server | Duplicada con SQL Server; no es parte de tu foco. |
| SQL Server | Igual que la anterior. |
| Servicios web | Duplicada con "Servicios web de RESTful". |
| Web Services | Duplicada con "Servicios web de RESTful". |
| Infraestructura de software | Generica; queda cubierta por Docker, AWS y CI/CD. |

Opcionales: jQuery y Optimizacion para motores de busqueda (SEO). Tienen validaciones, pero no suman al posicionamiento. Si las dejas, que queden al final.

### Agregar

| Categoria | Aptitudes |
|---|---|
| Frontend | TypeScript, Material UI, Apollo GraphQL, Vite, React Native |
| Backend | NestJS, API REST (si "Servicios web de RESTful" no alcanza) |
| Arquitectura | Arquitectura de software, Clean Architecture, Domain-Driven Design (DDD) o Command Query Responsibility Segregation (CQRS), segun cual exista en LinkedIn |
| IA | Large Language Models (LLM), Inteligencia artificial generativa, OpenAI API, Google Gemini, Ingenieria de prompts (Prompt Engineering) |
| Automatizacion | Google Apps Script, Automatizacion de procesos, Twilio |
| DevOps | Docker, GitHub Actions, Amazon Web Services (AWS), Integracion continua y entrega continua (CI/CD) |
| Interpersonales | Comunicacion con clientes, Mentoria (si aplica) |

### Corregir asociaciones

Socket.io, Mongoose y Express.js figuran asociadas a Doppler, pero las usaste en CUTI y News Kiosk. Asocialas a 404 Crafters o al periodo de crecimiento profesional.

## 6. Idiomas

Cambiar Ingles de "Competencia basica profesional" a **"Competencia profesional"**. Completaste tres anos de curso y trabajas a diario en ingles con clientes. Si preferis ser conservador, "Competencia profesional limitada" queda alineado con el "Upper-Intermediate en progreso" del CV.

## 7. Destacado (seccion nueva)

1. **CV online**: enlace a https://hcardoso81.github.io/professionalIdentity/ con el titulo "CV - Senior Full Stack & Applied AI Engineer".
2. **Publicacion sobre Insider Automation** (ver seccion 9), cuando la publiques.
3. **Publicacion sobre el asistente de WhatsApp**, con un video corto o una captura de una conversacion, sin datos personales.

## 8. Recomendaciones

Las 10 actuales cubren muy bien liderazgo, adaptabilidad, Clean Code y trato con clientes. Para que tambien respalden el perfil actual:

- **Ezequiel Perotta**: su recomendacion es de 2023 y habla de PHP y WordPress. Hoy trabajan juntos en Portal Expensas y en el asistente de WhatsApp; pedile una nueva enfocada en React, arquitectura e IA.
- **Lina Lujan Pontoriero (Insider)**: su recomendacion de 2025 es previa a Insider Automation. Si te escribe otra, que mencione el pipeline de IA.
- **Organizador de Mundialito Senior**: pedile una recomendacion como cliente sobre el asistente.

## 9. Actividad: publicacion sugerida

Una publicacion concreta sobre un proyecto real rinde mucho mas que la actividad actual. Borrador:

```text
How do you put AI into an editorial newsroom without losing control?

For Insider Latam, I built a pipeline that turns press releases received by email into WordPress drafts. Three decisions made the difference:

1. Start cheap. The first version was a Zapier + Gemini POC. It proved the idea in days, and also showed its limits.
2. Re-architect on purpose. I moved it to Google Apps Script + Gemini API: resumable batches, idempotent attempts and prompts versioned in a spreadsheet, so editors can change them without a deploy.
3. Keep a human in the loop. The system only creates drafts. Nothing gets published without an editor's review.

AI is not the hard part. Reliability is.

#AppliedAI #Automation #GoogleAppsScript #Gemini #WordPress
```

Antes de publicarla, confirma con Insider que esta de acuerdo con mostrar el proyecto.

## 10. Ajustes menores

- **Aplicaciones vinculadas**: saca las que no uses (HubSpot, IntelliJ IDEA, Gamma, Replit Agent) y agrega las que si, si estan disponibles (por ejemplo VS Code o GitHub).
- **Tengo interes en...**: decidi si activas "Open to work" visible solo para reclutadores. Es una decision tuya; no la cambie en ningun documento.
- **Informacion de contacto**: agrega el CV online como sitio web.

## 11. Orden sugerido para aplicar

1. Acerca de y aptitudes principales.
2. Nuevas experiencias: Insider Latam, Mundialito Senior e IntermarketFlow.
3. Edicion de 404 Crafters, Crecimiento profesional y Doppler.
4. Aptitudes: quitar, agregar y reasociar.
5. Proyectos y Destacado.
6. Idioma ingles.
7. Pedidos de recomendacion y primera publicacion.
