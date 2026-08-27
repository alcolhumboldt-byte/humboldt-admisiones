# HANDOFF — Landing de Admisiones, Colegio Humboldt

## Objetivo
Landing publicitaria de una sola página para captar familias interesadas en matricular. Meta única: que el acudiente escriba por WhatsApp.

## Estado actual
Existe `index.html`: archivo único, HTML + CSS + JS inline, sin dependencias ni build. Diseño terminado y responsive. Falta contenido real y despliegue.

## Stack
- Estático puro. No usar framework, la página no lo necesita.
- Despliegue: Vercel conectado a un repo de GitHub. Sin build step.
- Fuentes: Google Fonts, **Archivo** (display) + **Source Sans 3** (texto). Dos familias, no tres.

## Dirección de diseño: fotográfico institucional
Rediseñada tomando como referencia thewalkerschool.org. Reglas que hay que respetar al editar:

- **La fotografía es el diseño.** El sitio de referencia son 66 fotos; su estética *es* la fotografía. Cada slot vacío o con placeholder de stock resta más de lo que parece. Sin fotos reales esta página no funciona: es la tarea número uno, por encima de cualquier ajuste visual.
- **Display: grotesca pesada en versalitas.** Archivo 800, `line-height:.94`, tracking negativo. El titular hace el trabajo pesado. Nada de serif: el proyecto salió de una dirección editorial con serif y no se vuelve a ella sin decisión explícita.
- **El índigo es el color de marca dominante**, en el papel que el granate cumple en la referencia: campos completos (banda de cifras, tarjetas de laboratorios, bloque de logro, footer) y color de marca en titulares de subsección. No es un acento diluido sobre cada elemento.
- **Un solo sistema de esquinas: radio 0.** Botones, inputs y fotos, todo rectangular. La única excepción es el botón flotante de WhatsApp, que es circular.
- **Presupuesto de rótulos: 3 en toda la página** (hero, laboratorios, contacto). El rótulo es la versalita pequeña sobre el titular. Ponerlo en cada sección es la firma más reconocible de página hecha por IA. Si agregas una sección, no le pongas rótulo: el titular ya nombra la sección.
- **Sin rayas em ni en (`—`, `–`) en ningún texto visible.** Coma, punto o dos puntos. Es la otra firma delatora.
- **El texto se gana su lugar.** Un acudiente escanea, no lee. Titulares de 8 palabras o menos, párrafos de 25 o menos. El titular del hero es de 2 líneas en escritorio: es una regla dura, no una preferencia.
- **Familias de layout, una vez cada una.** Hero a sangre, banda de cifras, rejilla asimétrica de tarjetas foto, lista rayada, declaración grande + campo índigo, mosaico a sangre, pasos numerados, formulario a dos columnas, acordeón. No repetir una familia en dos secciones.

## Estructura de la página
1. Nav sticky (anclas en versalitas + CTA)
2. Hero: foto a sangre + titular gigante encima + CTA WhatsApp
3. Banda de 3 cifras sobre campo índigo
4. `#formacion` — rejilla asimétrica de 3 tarjetas foto con numeral calado; la de I+D ocupa el campo ancho
5. `#niveles` — lista editorial de 4 filas con reglas; cada fila abre WhatsApp con mensaje distinto
6. `#laboratorios` — **sección diferenciadora**. Declaración grande + 3 tarjetas índigo + CTA. Es el gancho de venta.
7. `#instalaciones` — dos listas rayadas + bloque índigo del logro deportivo, seguido del **mosaico de fotos a sangre**
8. `#admision` — 4 pasos numerados
9. `#contacto` — CTA WhatsApp + formulario de 3 campos
10. `#faq` — acordeón (`<details>`)
11. Footer índigo + botón WhatsApp flotante

Nota: el nav lista 5 secciones y colapsa a hamburguesa por debajo de 1020px. Al agregar otra, quitar una antes.

## Convenciones del código
- Todo elemento con clase `.wa` recibe el link de WhatsApp automáticamente. El texto prellenado sale del atributo `data-msg`. Para agregar un CTA nuevo: `<a href="#" class="wa" data-msg="...">`.
- Variables CSS en `:root`. No hardcodear colores.
- **`--tinta` es fondo, `--marca-txt` es primer plano.** El índigo de marca sobre papel se pinta con `--marca-txt`, que se aclara en modo oscuro; `--tinta` se queda para campos de fondo. Usar `--tinta` como color de texto rompe el contraste en oscuro.
- **Modo oscuro por `prefers-color-scheme`**, resuelto conmutando tokens en un solo bloque `@media`. Verificado: todo el texto pasa WCAG AA en ambos modos (mínimo medido 5.16:1 en claro).
- El mosaico de `#instalaciones` es hijo directo de `<section>` y va a sangre sin `100vw`: ese truco incluye el ancho de la barra de scroll y desplaza la rejilla unos píxeles. La rejilla tiene **8 celdas exactas**; si cambias el número de fotos, reajusta los `span` para que no quede ninguna vacía.
- Clase `.rv` = animación de aparición al hacer scroll (IntersectionObserver). Respeta `prefers-reduced-motion`. Poner `.cascada` en el contenedor para escalonar los hijos.
- Marcadores `[ ... ]` = contenido pendiente por reemplazar.
- El estado del nav al hacer scroll usa un **centinela de 1px + IntersectionObserver**, no un listener de `scroll`: ese listener corre en cada frame y el navegador no lo batchea.
- **Animación:** curvas en `--ease-out` (entradas/salidas) y `--ease` (hover/color). Feedback de pulsación a 160ms. Todo `:hover` va dentro de `@media (hover: hover) and (pointer: fine)` para que no se dispare al tocar en móvil. `prefers-reduced-motion` conserva opacidad y color, elimina solo el movimiento.

## Tareas pendientes

### Bloqueantes para lanzar
1. **Las 12 fotos.** Hoy son placeholders de `picsum.photos`, buscar `TODO FOTO` en el HTML. Ninguna puede salir a producción: son fotos de stock de gente ajena al colegio en una página de admisiones. Slots, con sus medidas:
   - `1/12` hero, horizontal 2400×1400
   - `2/12` I+D, 1600×900
   - `3/12` rigor académico, 1200×900
   - `4/12` vida escolar, 1200×900
   - `5/12` a `12/12` mosaico: la primera 1600×1600, la sexta 1800×900, el resto 900×900
   Con la dirección de diseño actual esto no es cosmético. La página *es* las fotos.
2. `const TEL` en el `<script>` final → número institucional, formato `57XXXXXXXXXX`, sin `+` ni espacios.
3. `const ENDPOINT` → URL para guardar los leads del formulario. Si queda vacío, el formulario abre WhatsApp con los datos prellenados (fallback funcional, sirve para lanzar).
4. Laboratorios: la sección quedó como declaración sola, sin ejemplos. Las tres tarjetas de proyecto se quitaron por decisión del colegio (26 ago 2026) en vez de dejarlas con texto de relleno. Hoy la sección afirma el método pero no lo demuestra: si aparecen proyectos reales con grado y año, recuperar el bloque `.labs-grid` del commit `2181a11` y volver a montarlo. Es la prueba que más peso tendría en toda la página.
5. FAQ: costos, cupos, documentos de matrícula, ingreso a mitad de año.
6. Footer: dirección real, correo real, horario real.
7. ~~Instalaciones: año y categoría del campeonato.~~ Resuelto: el bloque `.logro` ya no cuelga de un campeonato sin fecha. Ahora nombra los logros que dio el colegio: pruebas ICFES, Olimpiadas Matemáticas y seis disciplinas deportivas.
8. Instalaciones: preguntar al colegio qué escenarios deportivos tienen (cancha, coliseo, polideportivo) — hay equipo campeón pero el espacio no está listado porque nadie lo confirmó. Tampoco se inventó.
9. ~~Logo y colores oficiales del colegio.~~ Hecho: paleta tomada del logo oficial, familia índigo/morado. Los tokens vigentes son `--tinta` #211C6C, `--morado` #6D68B0 y `--lavanda` #B7B3E3 (los nombres viejos `--verde` y `--marigold` ya no existen). Falta insertar el logo real como imagen: hoy en el nav y el footer solo está el nombre en texto.

### Abiertos por el contenido nuevo
- **Nombre del colegio.** La página dice "Colegio Alejandro **de** Humboldt"; el texto que entregó el colegio lo escribe cuatro veces como "Colegio Alejandro Humboldt", sin el "de". Confirmar cuál es el nombre oficial. Aparece en el `<title>`, el nav, el footer y la meta description.
- **Cómo se reserva el cupo de verdad.** Los botones dicen "Reserva tu cupo" y hoy todos abren WhatsApp. El texto del colegio describe un formulario de admisión propio. Si ese formulario existe, decidir si el botón lleva allí en vez de a WhatsApp.
- **Nombre de los laboratorios.** El HANDOFF fijó "Laboratorios de Investigación y Desarrollo"; el colegio los llama "Laboratorios de Química e Innovación". Hoy la sección usa el segundo en el cuerpo pero conserva el posicionamiento del primero. Unificar.
- **Confirmar el "6"** de disciplinas deportivas en la banda de cifras. El colegio escribió "incluyendo", así que pueden ser más.
- Faltan dos cifras reales para esa banda si se quieren números: años de trayectoria y número de estudiantes.

### Después del lanzamiento
- Backend del formulario: tabla en Supabase (`nombre`, `tel`, `grado`, `created_at`) + notificación.
- SEO: `og:image`, favicon, JSON-LD tipo `School`.
- Autoalojar las fuentes. Hoy entran por `<link>` a Google Fonts, que cuesta una conexión extra antes de que pinte el texto. Se mitigó con `preconnect`, pero si algún día hay build step o se aceptan archivos junto al HTML, descargar los woff2 y servirlos con `@font-face` + `font-display:swap`.
- Pixel de Meta para pauta pagada.
- Testimonios reales de padres (aún no existen en la página).

## Decisiones ya tomadas — no rediscutir
- WhatsApp es la acción principal, no el formulario. El formulario es respaldo para quien escribe fuera de horario.
- El área de tecnología se vende como **Laboratorios de Investigación y Desarrollo**, nunca como "clase de sistemas" ni como "los estudiantes hacen apps". Se vende el método, no el producto.
- Sin CMS. El contenido se edita directo en el HTML.

## Advertencias
- ~~Nombre del tercer pilar.~~ Resuelto: el colegio lo llama **Formación en valores cristianos**. Así quedó en la página.
- Definir quién responde el WhatsApp y en qué horario **antes** de lanzar. Un lead sin respuesta en menos de 5 minutos se enfría; sin eso la página no sirve.
- Nada de lo que está en `[ ... ]` puede salir a producción.
