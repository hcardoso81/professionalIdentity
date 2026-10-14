# Guía de estilo para documentos de cliente

Formato base para manuales, presentaciones y casos de prueba que se entregan a un cliente en Google Docs. El objetivo es un documento sobrio, legible y con aire: jerarquía de títulos clara, interlineado generoso y separación consistente entre texto e imágenes.

El primer documento con este formato fue el manual de Insider Shorts.

---

## 1. Estructura del documento

Se usa una pestaña de Google Docs por audiencia o propósito:

| Pestaña | Contenido | Lector |
|---|---|---|
| **Presentación** | Qué es, objetivo, funcionalidades, requisitos del sistema | Cliente / decisor |
| **Manual de usuario** | Paso a paso por pantalla, con captura de cada una y un ejemplo completo de punta a punta (alta → resultado en el sitio) | Editor / administrador |
| **Casos de prueba** | Configuración base + un caso por combinación relevante, cada uno con pasos, resultado esperado y captura | QA / cliente técnico |

Reglas generales:

- Cada pestaña abre con un **Título** y un **Subtítulo** de una línea que dice para qué sirve esa pestaña.
- Las secciones (H1) responden a una pregunta del lector: "¿Qué hace?", "¿Cómo agrego una playlist?".
- Una captura por concepto, siempre debajo del texto que la explica, nunca antes.
- Nada de jerga interna (nombres de clases, hooks, rutas de código) en Presentación ni en Manual.

---

## 2. Paleta

| Uso | Color | Hex |
|---|---|---|
| Primario (título, H1, bordes fuertes) | Violeta | `#604c8d` |
| H3 / acentos | Violeta oscuro | `#4b3a70` |
| Bordes suaves (línea bajo H1) | Lavanda | `#e4def0` |
| Fondo de recuadros destacados | Lavanda muy claro | `#f3f0f9` |
| H2 | Tinta | `#2d2d34` |
| Texto de cuerpo y listas | Gris oscuro | `#3d3d42` |
| Subtítulo, epígrafes, notas | Gris medio | `#6b6b73` |

Si el cliente tiene color de marca propio, reemplazar solo el **primario** y derivar el oscuro (≈ 20 % más oscuro) y los lavandas (mismo tono, 10 % y 5 % de saturación sobre blanco). Los grises no cambian.

---

## 3. Tipografía y jerarquía

Fuente única: **Lato** en todo el documento (disponible en Google Docs, buena lectura en pantalla y en PDF). Alternativas equivalentes: Inter, Source Sans 3.

| Nivel | Tamaño | Peso | Color | Espacio arriba | Espacio abajo | Interlineado | Extra |
|---|---|---|---|---|---|---|---|
| Título | 32 pt | Bold | Primario | 0 | 6 pt | 1,10 | — |
| Subtítulo | 14 pt | Regular | Gris medio | 0 | 28 pt | 1,25 | Borde inferior 2 pt primario, padding 14 pt |
| H1 | 22 pt | Bold | Primario | 34 pt | 12 pt | 1,15 | Borde inferior 1 pt lavanda, padding 6 pt |
| H2 | 16 pt | Bold | Tinta | 26 pt | 8 pt | 1,15 | — |
| H3 | 13 pt | Bold | Violeta oscuro | 20 pt | 6 pt | 1,15 | — |
| Párrafo | 11 pt | Regular | Gris oscuro | 0 | 10 pt | **1,45** | — |
| Ítem de lista | 11 pt | Regular | Gris oscuro | 0 | 6 pt | 1,40 | — |

Todos los títulos llevan **"Mantener con el siguiente"** para que nunca queden huérfanos al pie de página.

Principio: el espacio *arriba* de un título siempre es mayor que el de *abajo*, así el título queda pegado a su contenido y separado de lo anterior.

---

## 4. Imágenes y epígrafes

| Elemento | Alineación | Arriba | Abajo | Interlineado | Extra |
|---|---|---|---|---|---|
| Párrafo de imagen | Centrado | 16 pt | 6 pt | 1,00 | Mantener con el siguiente |
| Epígrafe | Centrado | 0 | **24 pt** | 1,15 | Gris medio, 9 pt, cursiva |

- El epígrafe va siempre debajo de la imagen y describe qué se ve ("Pestaña Configuración con autoplay activado"), no repite el título.
- Las 24 pt bajo el epígrafe separan cada bloque imagen + epígrafe del siguiente contenido.
- Ancho de imagen: 720 pt para capturas de escritorio (en pageless con ancho "Ancho" la columna mide ≈ 910 pt, así que quedan al 80 %). Capturas de tablet 390 pt y de móvil 260 pt. No mezclar tamaños dentro de una misma sección.
- El ancho de imagen se fija al insertarla: la API no permite redimensionar una imagen existente, solo borrarla y volver a insertarla. Elegir el ancho antes de insertar.
- Capturar a una resolución que soporte ese ancho sin verse borrosa: al menos 1000 px de ancho para 720 pt (en frontend, usar `deviceScaleFactor: 2` si el viewport es angosto).

### Capturas de pantalla

- Viewport fijo para todas las capturas de un mismo documento (admin: 1440 × 900; frontend: 1280 de ancho).
- Recortar al área relevante; sin barra del navegador, sin pestañas, sin notificaciones de otros plugins.
- Datos reales o creíbles, nunca "test", "asdf" ni lorem ipsum.
- No mostrar API keys, emails ni datos personales; si aparecen, rehacer la captura.
- Nombrar los archivos por orden y contenido: `03-agregar-playlist-formulario.png`.

---

## 5. Recuadros destacados

Para información que el lector debe tener presente durante varias secciones (por ejemplo, la "Configuración base" de los casos de prueba):

- Fondo `#f3f0f9`
- Borde izquierdo 3 pt primario, padding 10 pt
- Sangría 4 pt a ambos lados
- 6 pt arriba, 16 pt abajo

Usar como máximo uno por sección. Si todo está destacado, nada lo está.

---

## 6. Redacción

- Segunda persona, tono directo: "Pegá la URL de la playlist" / "Pegue la URL…" según el registro acordado con el cliente; no mezclar.
- Pasos numerados para acciones; viñetas para listas de opciones o características.
- Nombres de botones y campos en **negrita** y escritos exactamente como aparecen en pantalla.
- Shortcodes, URLs y valores literales en fuente monoespaciada.
- Párrafos de 2 a 4 líneas. Si un párrafo pide más, probablemente son dos ideas.
- Cada caso de prueba sigue el mismo esquema: **Objetivo**, **Configuración**, **Pasos**, **Resultado esperado**, captura.

---

## 7. Receta técnica (Google Docs API)

Para generar o reformatear el documento desde código con el conector de Google Docs:

1. **Contenido primero, formato después.** Insertar todo el texto, luego las imágenes, y recién al final aplicar estilos. Los estilos no mueven índices; las inserciones sí.
2. **Formato directo por párrafo.** La API no permite modificar los estilos con nombre (Título, Encabezado 1…). Se aplica `updateParagraphStyle` + `updateTextStyle` sobre cada rango. Agrupar párrafos consecutivos del mismo tipo en un solo request.
3. **Índices en UTF-16.** Los caracteres fuera del BMP (emoji) ocupan 2 posiciones. Cada imagen inline ocupa 1 posición.
4. **Pestañas.** Cada request lleva `tabId` en su rango.
5. **Control de revisión.** Cada batch con `writeControl.requiredRevisionId`; si se rechaza, releer y reconstruir.
6. **Imágenes.** `insertInlineImage` necesita una URL pública. Para capturas locales: servir la carpeta con un servidor estático + túnel temporal de Cloudflare (`cloudflared tunnel --url`). El túnel gratuito de ngrok **no sirve** (su página intermedia rompe la descarga de Google). Insertar en lotes de 4–5 imágenes; lotes grandes fallan de forma intermitente. Cerrar el túnel al terminar.
7. **Documento sin páginas (pageless).** Los márgenes no se pueden fijar por API. El ancho del texto es una preferencia de vista de cada usuario (no queda en el documento ni en la API): se ajusta a mano en **Ver → Ancho del texto → Ancho**. "Medio" deja una columna de ≈ 470 pt y desperdicia la mitad de la pantalla. Si el cliente va a imprimir o exportar a PDF, pasar a formato con páginas (**Archivo → Configuración de página → Páginas**) con márgenes de 2,5 cm.

El generador usado en el manual de Insider Shorts (`restyle.py`) implementa exactamente las tablas de las secciones 3, 4 y 5: un diccionario por nivel de título y por tipo de bloque, y una pasada que convierte la lista de párrafos en requests.

---

## 8. Checklist antes de entregar

- [ ] Las tres pestañas abren con Título + Subtítulo.
- [ ] Ningún título quedó solo al pie de página (revisar en vista con páginas o exportando a PDF).
- [ ] Todas las imágenes tienen epígrafe y el mismo ancho dentro de su sección.
- [ ] Ninguna captura muestra datos sensibles ni avisos de terceros.
- [ ] Nombres de botones y campos coinciden con la versión entregada del producto.
- [ ] Ancho de texto en "Ancho" (pageless) o márgenes de 2,5 cm (con páginas). Avisar al cliente que lo elija en **Ver → Ancho del texto**, porque es una preferencia de cada lector.
- [ ] Permisos del documento: el cliente con acceso de lector o comentador, no editor.
