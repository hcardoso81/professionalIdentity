# Hernan Federico Cardoso

Senior Full Stack Engineer | React & TypeScript | Clean Architecture | Applied AI & Automation

Tandil, Argentina  
+54 2494619638  
hernan.f.cardoso@gmail.com  
LinkedIn: https://www.linkedin.com/in/cardosohernan/  
CV online: https://hcardoso81.github.io/professionalIdentity/

## Professional Summary

Senior Full Stack Engineer with 18+ years of experience building, maintaining and modernizing production web applications.

Focused on React and TypeScript for complex administrative platforms and B2B portals, using Clean Architecture, CQRS and Presenter Pattern, with GraphQL/REST integrations and Docker-based delivery on GitHub Actions and AWS.

In 2026, built applied AI systems for clients: an editorial automation pipeline on Google Apps Script and the Gemini API that turns press releases into WordPress drafts with human review, and a WhatsApp assistant with OpenAI function calling and answer checks against real data.

Strong background in PHP and WordPress plugin development, legacy modernization and AI-assisted development with coding agents. Recognized for technical ownership, clear communication and a collaborative mindset with teams and clients.

## Technical Skills

Languages: TypeScript, JavaScript, PHP, SQL, HTML, CSS.

Frontend: React, Vite, Material UI, MUI X DataGrid, Apollo Client, React Router, React Query, React Hook Form, Zod, i18next.

Backend / Data: Node.js, NestJS, Express, REST APIs, GraphQL (Apollo, subscriptions over WebSocket), PostgreSQL, MongoDB, MySQL, JWT.

AI / Automation: Generative AI, LLMs, Gemini API, OpenAI API, function calling, structured outputs, multimodal analysis, hallucination guardrails, human-in-the-loop, Google Apps Script, Gmail/Drive/Docs/Sheets APIs, Twilio WhatsApp API, Zapier, AI-assisted development (Claude Code, Codex).

Architecture: Clean Architecture, Hexagonal Architecture, CQRS, Presenter Pattern, use cases, repositories, mappers, ADRs, SOLID.

WordPress: Plugin development, REST API, WP-Cron, custom tables, ACF, Custom Post Types, nonces/capabilities, rate limiting, PhpSpreadsheet, Mailchimp, LinkedIn OAuth, YouTube Data API, PHP 8 migrations.

DevOps: Docker, GitHub Actions, GitLab CI/CD, GitHub Container Registry, AWS (Lightsail, S3), Vercel, Traefik, NGINX, PM2.

Mobile: React Native, Expo.

## Professional Strengths

- Leadership and ownership: experienced leading teams, coordinating delivery, removing blockers and taking responsibility for product quality and technical outcomes.
- Communication and client-facing work: comfortable explaining technical concepts, aligning with stakeholders, presenting demos and writing client-facing documentation.
- Problem solving: pragmatic approach; validate ideas with low-cost POCs, then decide explicitly when to re-architect, balancing quality, time and business needs.
- Autonomy and teamwork: proactive, reliable and able to work without close supervision while keeping a positive, collaborative and supportive team dynamic.

## Professional Experience

### 404 Crafters - Senior Full Stack Engineer

November 2023 - Present
https://www.proyecto404.com/

- Develop and maintain production web applications for international clients, focused on React, TypeScript and complex business workflows.
- Apply layered architectures (Clean Architecture, CQRS, Presenter Pattern) separating presentation, domain, use cases and infrastructure.
- Configure AWS environments and CI/CD workflows with GitHub Actions, Docker and Docker Compose to support delivery and deployment.
- Collaborate directly with clients and teammates in English to clarify requirements, discuss technical decisions and deliver maintainable solutions.

Key projects:

- Portal Expensas: condominium management platform covering settlements, payroll, payments, units, suppliers, documents and internal support tickets. Interfaces and business workflows with React, TypeScript, Material UI, MUI X DataGrid and Apollo GraphQL, including realtime tickets over GraphQL subscriptions.
- Portal de Aliados - Fanki: B2B portal for event operations, sales, payments, attendance and business metrics. Dashboards, exportable reports and role-based interfaces with React, TypeScript, Vite and Material UI.
- News Kiosk: news analysis platform for a US client, across frontend and backend. Search interfaces, dashboards, saved searches, PDF viewing and email sharing with React, React Query, Node.js, Express and MongoDB.

### Insider Latam - Full Stack & AI Automation Developer (Freelance)

October 2024 - Present
insiderlatam.com

- Insider Automation: built an AI editorial pipeline that transforms press releases received by email, with their attachments and linked documents, into WordPress drafts for human review. Validated the idea with a Zapier + Gemini POC, then rebuilt it on Google Apps Script and the Gemini API with resumable batch processing, idempotent retries, prompts editable from Google Sheets and a WordPress control panel. Editors stay in control of every publication.
- Develop custom WordPress plugins and integrations: a responsive newsletter builder, LinkedIn company-page publishing, editorial filters with Excel export, a YouTube Shorts carousel, and sports and event coverage widgets.
- Maintain and modernize the site: PHP upgrades, plugin updates, troubleshooting and performance improvements, working directly with the client on requirements.

### Mundialito Senior - Full Stack & AI Developer (Freelance)

March 2026 - July 2026

- Developed a WhatsApp AI assistant for a client running amateur football tournaments, so participants and organizers can ask about fixtures, results, standings, teams and rules in natural language.
- Backend with NestJS, TypeScript, PostgreSQL and Twilio, integrating OpenAI function calling with seven tools over the CopaFacil API and a Google Docs FAQ.
- Request signature validation, retries, API fallbacks and response checks against tool results to reduce unsupported answers, plus admin tools and a testing environment that uses the same processing pipeline.
- Demonstrated to the client with positive feedback; launch is pending on the client's side.

### IntermarketFlow - WordPress Plugin Developer (Freelance)

August 2025 - Present
intermarketflow.com

- Develop and maintain SEO Content Locker, a custom WordPress plugin for premium content access and lead capture on a financial markets analysis website.
- Email-based access with trial expiration, layered anti-bot protection (reCAPTCHA v3, rate limiting by IP, form and email), Mailchimp integration with lead-source tracking, lead management, CSV exports and daily WP-Cron reports.
- Refactored procedural code into modular PHP services, repositories and an event-based notification system.

### Freelance / Professional Growth Period - Mobile and React Developer

March 2023 - November 2023

- Transitioned to React, TypeScript, React Native, Hexagonal Architecture and Clean Architecture.
- Worked on CUTI, a mobile app for corporate conference calls with live audio (Agora RTC), Socket.IO realtime sync, moderation, PDF viewing and recordings.

### Doppler - Senior WordPress Developer / Frontend Developer / Scrum Master

April 2013 - February 2023

- Led maintenance and evolution of 5 institutional WordPress websites for marketing, internal requests and integrations.
- Worked as technical reference and collaborated with company teams to research, prioritize and design new functionality.
- Contributed to GOEMMS, a major marketing event in Latin America: high-traffic website support, live streaming flows and Twitter API integration with caching.
- Handled hosting maintenance, migrations, performance improvements and external API integrations.

### Intercomgi - Scrum Master / Frontend Developer

April 2012 - April 2013

- Scrum Master and frontend developer for a JavaScript single-page web application.

### Avatar - Project Lead / Scrum Master / Senior PHP Developer

March 2008 - June 2012

- Led and developed PHP websites for major clients in Latin America, including Greenpeace Latin America, Mastercard, Banco Nacion Argentina, Fashion TV, Disney, Coca-Cola, Sherwin Williams and Telcosur.
- Coordinated development teams and ensured delivery quality.

## Selected Projects

### Insider Automation - Editorial AI Pipeline

Press releases from Gmail, with attachments and linked Google Docs, processed by Google Apps Script and the Gemini API into WordPress drafts. Resumable batches that work around platform execution limits, idempotent retries, prompts editable without deploys, featured-image suggestions and mandatory human review. Built on documented architecture decisions and a local test suite.

### WhatsApp AI Tournament Assistant

Conversational assistant built for an amateur football tournament organizer with NestJS, Twilio, OpenAI, PostgreSQL, Google Docs and the CopaFacil API. Multi-tournament sessions, seven function-calling tools, live data with fallback and checks that fall back to a safe answer when a response is not supported by the data. Demonstrated to the client; launch pending on their side.

## Education

Software Engineer Degree - UNICEN  
Graduated, 2015

## Languages

Spanish: Native  
English: Upper-Intermediate in progress. Able to work with technical documentation and collaborate with English-speaking teams.
