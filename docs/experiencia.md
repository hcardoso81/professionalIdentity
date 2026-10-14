# Experiencia Profesional - Timeline

Este documento organiza la experiencia por periodo, compania y proyectos asociados. Sirve como base para CV, LinkedIn, entrevistas y reconstruccion de carrera.

## 404 Crafters

Sitio: https://www.proyecto404.com/

Periodo: noviembre 2023 - actualidad.

Rol sugerido: Senior Frontend Engineer / Full Stack Engineer.

Nota sobre fechas: los periodos por proyecto se reconstruyeron a partir del historial de commits. Hubo solapamientos durante las transiciones entre proyectos.

### Mayo 2025 - actualidad

Proyecto principal: Portal Expensas Admins.

Responsabilidades:

- Desarrollo de una aplicacion administrativa React + TypeScript para gestion de consorcios y expensas.
- Definicion general de UI tomando como guia patrones del dashboard de Material UI.
- Segundo contribuidor del repositorio, con foco en sueldos/liquidaciones, unidades, recibos, amenities, juicios, polizas y el sistema de tickets Rocket.
- Tickets y conversaciones en tiempo real con GraphQL subscriptions sobre WebSocket, con reconexion y resincronizacion.
- Aplicacion de Clean Architecture, CQRS y Presenter Pattern; desde 2026 el repositorio compila varios portales desde un core compartido.
- Pipeline de despliegue con GitHub Actions, Docker, GitHub Container Registry, AWS Lightsail y Traefik, incluyendo flujo de hotfixes por tags.
- Integracion con GraphQL, Apollo, Material UI, MUI X DataGrid, React Router e i18next.

### Agosto 2024 - abril 2025

Proyecto principal: Portal de Aliados.

Responsabilidades:

- Desarrollo de portal B2B para aliados de Fanki; principal contribuidor de la primera version del portal.
- Definicion general de UI y experiencia administrativa.
- Trabajo sobre dashboards, metricas, ventas, pagos, asistencias, eventos, comercios y reportes.
- Integracion de React, TypeScript, Vite, Material UI, MUI X, ApexCharts, React Hook Form, Zod e i18next.
- Participacion en flujos de despliegue con Node/Express, Docker, GitLab CI/CD, Vercel y Helm/Kubernetes.

### Noviembre 2023 - marzo 2025

Proyecto principal: News Kiosk.

Contexto:

- Trabajo con cliente nativo de Estados Unidos.
- Participacion en desarrollo full stack y planteo de UI.

Responsabilidades:

- Desarrollo y mantenimiento de plataforma full stack para busqueda, analisis y gestion de noticias; principal contribuidor del repositorio en ese periodo.
- Frontend en React + TypeScript con arquitectura por capas: Presentation, Domain y Data.
- Integracion de React Query, Axios, Material UI, rutas protegidas, dashboards, lectura de PDFs y busquedas guardadas.
- Backend con Node.js, Express, MongoDB, Mongoose, JWT, Nodemailer, Winston/CloudWatch y PM2.
- Automatizacion y despliegue con Docker y GitLab CI/CD.

## Freelance / IntermarketFlow

Sitio: intermarketflow.com.

Periodo: 2024 - actualidad.

Descripcion del negocio:

IntermarketFlow esta orientado a integrar analisis intermarket, tecnico y macroeconomico para generar oportunidades de trading en mercados financieros.

Responsabilidades:

- Desarrollo del plugin SEO Content Locker para WordPress.
- Mantenimiento del sitio y tareas evolutivas.
- Trabajo sobre monetizacion, captacion de leads, control de acceso a contenido premium e integracion con Mailchimp/reCAPTCHA.
- 2026: refactor del plugin hacia servicios, repositorios y namespaces; proteccion anti-bot por capas (reCAPTCHA v3 y rate limiting por IP, formulario y email); reporte diario de leads por WP-Cron; integracion con Elementor y landings.

## Insider Latam / Insider

Sitio: insiderlatam.com.

Periodo: 2023 - actualidad.

Responsabilidades:

- Mantenimiento del portal de noticias WordPress.
- Migracion del sitio a PHP 8.
- Desarrollo de plugins WordPress para necesidades editoriales y de marketing.
- Desarrollo de Insider Newsletters para creacion, renderizado y exportacion de newsletters HTML responsive.
- Desarrollo de WP2LinkedIn para publicacion controlada de posts en pagina de empresa de LinkedIn.
- Desarrollo de Welcome Popup Manager para popups configurables desde WP Admin.
- Desarrollo de WP Admin Posts Extended para filtros avanzados y exportacion editorial a Excel.
- Mantenimiento continuo del sitio: actualizacion de plugins, limpieza de logs de errores (mu-plugin para silenciar avisos inofensivos) y correcciones de rendimiento y scripts.
- 2026: Insider Automation, sistema de automatizacion editorial con IA. Primero un POC con Gmail, Zapier y Gemini (mayo 2026); luego reescritura sobre Google Apps Script, Gemini API, Drive, Sheets y WordPress REST API, con orquestacion reanudable por lotes, idempotencia, prompts versionados y plugin WordPress de control (agosto 2026 - actualidad). Validado en staging con una muestra real del cliente: 20 casos, 16 OK, 4 con advertencias, 0 errores.
- 2026: plugins Insider Shorts (carrusel de shorts desde playlists de YouTube), World Cup 2026 Widget (partidos del Mundial via API-Football) y Cannes Festival Medal Tracker (medallero de Cannes Lions importado desde Excel).
- 2026: evolucion de WP2LinkedIn (estados editables, reconexion de token), WP Admin Posts Extended (filtros por autor/ano, campo hasVideo) y plugins chicos de Edicion rapida.

## Mundialito Senior

Periodo: marzo 2026 - julio 2026.

Rol sugerido: AI / Full Stack Developer.

Proyecto principal: WhatsApp AI Tournament Assistant.

Responsabilidades:

- Diseño y desarrollo de un asistente conversacional para que participantes y organizadores consulten informacion del torneo directamente desde WhatsApp.
- Integracion del webhook de Twilio con validacion de firma HMAC-SHA1 y respuestas en TwiML.
- Implementacion de seleccion multi-torneo, memoria de sesion, normalizacion de consultas y tolerancia a errores de escritura.
- Diseño de un pipeline conversacional con routing por LLM, siete tools con function calling estricto y generacion de respuestas basada en resultados reales.
- Integracion de OpenAI, PostgreSQL, Google Docs como CMS de FAQ y CopaFacil API para datos sincronizados y consultas vivas.
- Implementacion de fallback ante fallas de CopaFacil y guarda anti-alucinacion para evitar respuestas no sustentadas.
- Desarrollo de herramientas administrativas para configurar torneos, sincronizar datos, revisar conversaciones y curar/ejecutar casos de testing.

## Prostagma - iniciativa propia (en desarrollo)

Periodo: julio 2026 - actualidad.

- Armado de una celula de desarrollo senior orientada a software a medida, IA, chatbots y automatizaciones.
- Copa Prostagma: SaaS multi-tenant para torneos de futbol (monorepo pnpm/Turborepo, NestJS, React, Next.js, PostgreSQL, Prisma), en etapa de bootstrap con ADRs.
- Prostagma AI Reports: plugin WordPress de reportes con adaptador opcional al WordPress AI Client.
- Todavia sin presencia publica: no incluir como empresa en CV/LinkedIn hasta que se lance.

## Freelance / Growth Period

Periodo: febrero 2023 - noviembre 2023.

Contexto:

Periodo de descanso profesional y reconversion tecnica hacia React, TypeScript, React Native, Laravel, arquitectura hexagonal y clean code.

Responsabilidades y aprendizajes:

- Desarrollo freelance en CUTI, aplicacion mobile de conference calls corporativas.
- Aprendizaje autodidacta de React, TypeScript y React Native.
- Profundizacion en arquitectura hexagonal, Clean Architecture y separacion por capas.
- Primeras practicas con Laravel.
- Inicio de cursos de ingles.

## Doppler

Periodo: abril 2013 - febrero 2023.

Rol: Senior WordPress Developer / Frontend Developer / Scrum Master.

Responsabilidades:

- Encargado de sitios institucionales de la empresa.
- Mantenimiento y evolucion de 5 sitios WordPress.
- Desarrollo de features para el area de marketing, pedidos internos e integraciones.
- Integracion con APIs externas y servicios de marketing.
- Mantenimiento de hosting, migraciones, performance y configuraciones tecnicas.
- Participacion en GOEMMS, evento de marketing relevante en Latinoamerica.

## Intercomgi

Periodo: abril 2012 - abril 2013.

Rol: Scrum Master / Frontend Developer.

Responsabilidades:

- Tareas de Scrum Master.
- Desarrollo frontend de aplicacion web.
- Trabajo con Backbone.js, JavaScript, MySQL y tecnologias web.

## Avatar

Periodo: marzo 2008 - junio 2012.

Rol: Lider de proyecto / Scrum Master / Lider de equipo / Senior PHP Developer.

Responsabilidades:

- Desarrollo de sitios PHP para clientes importantes de Latinoamerica.
- Liderazgo tecnico y coordinacion de equipos.
- Seguimiento de calidad de productos entregados.
- Mantenimiento y desarrollo para marcas y organizaciones como Greenpeace Latinoamerica, Mastercard, Banco Nacion Argentina, Fashion TV Project Runway Latinoamerica, Disney Highway Zapping Zone Latinoamerica, Coca-Cola, Sherwin Williams y Telcosur.

## Formacion Continua

- Cursos de ingles iniciados en 2023 y continuados durante 2024-2026.
- Ingles en progreso hacia B2.
- Aprendizaje autodidacta continuo en React, TypeScript, React Native, arquitectura hexagonal, Clean Architecture y mobile development.
- Desarrollo asistido por agentes de IA (Claude Code, Codex): cada proyecto propio incluye un `AGENTS.md` con reglas de arquitectura, seguridad y validacion, y documentacion de decisiones (ADRs) para trabajar con agentes de forma controlada.
