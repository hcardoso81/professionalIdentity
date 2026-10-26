# Busquedas de recruiters - Cobertura del perfil

Busquedas tipicas de LinkedIn Recruiter para los roles objetivo, revisadas contra el perfil publicado (relevamiento del 14 de octubre de 2026, ver [linkedin.md](linkedin.md)). Las busquedas estan en ingles porque asi buscan los recruiters de roles remotos internacionales.

Referencias:

- ✅ aparece: la busqueda encuentra el perfil.
- ⚠️ parcial: aparece solo en algunos casos, por ejemplo segun el filtro que use el recruiter.
- ❌ no aparece.

## Como cruza Recruiter las busquedas

- **Filtro por puesto** (Job title, actual o anterior): busca en el titulo de cada experiencia, no en el texto. Es el filtro mas usado. Recruiter puede sumar "titulos similares" si el recruiter lo activa.
- **Palabras clave**: busqueda booleana sobre headline, Acerca de, descripciones de experiencia, proyectos y aptitudes. En el texto la coincidencia es literal: "Next.js" no encuentra "NextJS".
- **Aptitudes**: catalogo normalizado. "React.js" y "React" cuentan como la misma aptitud.
- **Filtros adicionales**: ubicacion, anos de experiencia, idioma con nivel, "Open to work" y probabilidad de respuesta.

## 1. Senior Frontend Engineer

| Busqueda | Resultado | Por que |
|---|---|---|
| Puesto: `Frontend Engineer` OR `Frontend Developer` + keywords `React AND TypeScript` | ❌ | Ningun puesto dice "Frontend". El filtro por puesto deja el perfil afuera aunque el texto coincida. |
| `("frontend" OR "front-end") AND React AND TypeScript` (solo keywords) | ⚠️ | "frontend" aparece una sola vez, en la linea de News Kiosk. Coincide, pero con poca relevancia. |
| `React AND TypeScript AND ("Material UI" OR MUI) AND (dashboard OR "admin panel")` | ✅ | 404 Crafters: Material UI, dashboards, Portal Expensas. |
| `React AND (GraphQL OR Apollo)` | ✅ | Portal Expensas con Apollo GraphQL. |
| `React AND ("Next.js" OR NextJS)` | ❌ | Next.js no aparece. Solo se uso en Copa Prostagma, que todavia no es publico. No agregarlo hasta tener trabajo publicable. |
| `React AND (Jest OR "Testing Library" OR Playwright OR Cypress)` | ❌ | No hay testing frontend en el perfil. Es un pedido frecuente en roles senior de frontend. |

## 2. Senior Full Stack Engineer

| Busqueda | Resultado | Por que |
|---|---|---|
| Puesto: `Full Stack Engineer` OR `Full Stack Developer` + `React AND Node.js` | ✅ | Puesto actual en 404 Crafters, Insider Latam y Mundialito. |
| `"Full Stack" AND TypeScript AND (NestJS OR Express) AND (PostgreSQL OR MongoDB)` | ✅ | Mundialito (NestJS, PostgreSQL) y News Kiosk (Express, MongoDB). |
| Puesto: `Software Engineer` + `React AND TypeScript` | ⚠️ | Ningun puesto dice "Software Engineer". Solo aparece si el recruiter activa titulos similares. |
| `"software engineer" AND React` (solo keywords) | ❌ | La frase exacta no esta en el texto. |
| `(Docker OR AWS) AND ("GitHub Actions" OR "CI/CD") AND React` | ✅ | 404 Crafters y aptitudes. |

## 3. Applied AI / LLM Engineer

| Busqueda | Resultado | Por que |
|---|---|---|
| `(LLM OR "Large Language Models" OR "Generative AI") AND (OpenAI OR Gemini)` | ✅ | Aptitudes, Acerca de, Insider Latam y Mundialito. |
| `"function calling" OR "tool calling"` | ✅ | Mundialito y proyecto WhatsApp AI Tournament Assistant. |
| `"AI Engineer" OR "Applied AI"` (keywords) | ✅ | Headline. |
| Puesto: `AI Engineer` OR `Machine Learning Engineer` | ❌ | Ningun puesto lo dice. "Full Stack & AI Developer" solo entra con titulos similares activos. |
| `"prompt engineering"` | ❌ | No figura como aptitud ni en el texto, aunque los prompts versionados de Insider lo respaldan. |
| `RAG OR "retrieval augmented" OR embeddings OR "vector database" OR LangChain` | ❌ | No hay experiencia con RAG. Es de los filtros mas comunes en roles de IA. Es un hueco de experiencia, no de redaccion. |
| `(agents OR agentic) AND (OpenAI OR LLM)` | ⚠️ | Solo "AI coding agents" en el Acerca de, que habla de agentes de codigo y no de construir agentes. |

## 4. WordPress / PHP (posicionamiento secundario)

| Busqueda | Resultado | Por que |
|---|---|---|
| `WordPress AND ("plugin development" OR "custom plugin") AND PHP` | ✅ | IntermarketFlow, Insider Latam y Doppler. |
| Puesto: `WordPress Developer` | ✅ | IntermarketFlow y Doppler. |

## 5. Filtros generales

| Filtro | Resultado | Comentario |
|---|---|---|
| Ubicacion Argentina / Latin America | ✅ | Tandil, Argentina. |
| Remoto | ✅ | Acerca de: "Working remotely with international teams". |
| Anos de experiencia 10+ | ✅ | Historial desde 2008. |
| Idioma ingles con nivel "Professional working" o superior | ❌ | El perfil dice "Competencia basica profesional". Los recruiters que filtran por nivel de ingles no lo ven. |
| Open to work (solo recruiters) | ⚠️ | Sin decidir. Es una de las senales que mas pesa en Recruiter. |
| Busquedas en espanol (`"desarrollador full stack"`, `"desarrollador React"`) | ⚠️ | El perfil esta casi todo en ingles. Solo Avatar e Intercomgi siguen en espanol. LinkedIn permite agregar un perfil secundario en espanol. |

## 6. Cambios propuestos

### De redaccion (sin inventar experiencia)

1. **Frontend en un titulo**: si se apunta a roles de frontend, cambiar 404 Crafters a `Senior Full Stack Engineer (Frontend focus)` o `Senior Frontend / Full Stack Engineer`. Si cambia en LinkedIn, actualizar tambien el CV.
2. **"Software engineer" en el Acerca de**: primera linea `I'm a senior software engineer (full stack) with 18+ years...`.
3. **"Frontend" en el texto**: en 404 Crafters, `...with a focus on frontend architecture, React, TypeScript, and complex business workflows.`
4. **Aptitud Prompt Engineering**: la respaldan los prompts versionados de Insider Automation.
5. **Open to work solo para recruiters**: titulos Senior Frontend Engineer, Senior Full Stack Engineer, Senior Software Engineer y Applied AI Engineer, en modalidad remota.
6. **Ingles**: revisar el nivel (ver seccion 6 de [linkedin.md](linkedin.md)). Es la decision de mayor impacto en filtros de roles remotos.
7. **Perfil secundario en espanol**: opcional, para recruiters de LATAM que buscan en espanol.

### Huecos reales (requieren trabajo, no redaccion)

- **Testing frontend** (Jest, React Testing Library, Playwright): agregar tests a un proyecto publicable.
- **Next.js**: cuando Copa Prostagma sea publico.
- **RAG / embeddings**: un proyecto chico, por ejemplo busqueda semantica sobre el archivo de noticias de Insider, si el cliente esta de acuerdo.
