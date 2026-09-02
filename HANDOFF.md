# HANDOFF — Landing de Admisiones, Colegio Alejandro de Humboldt

## Objetivo
Landing de una sola página para captar familias interesadas en matricular.
Meta única: que el acudiente escriba por WhatsApp.

## Estado actual, 31 ago 2026

Trabajo hecho en la rama **`humboldt-kids`**, tres commits por encima de `main`:

```
fb17d55  Usa ilustraciones de undraw en Humboldt Kids
b77d071  Da fondo de marca al hero mientras no exista la foto
bd6cf46  Añade Humboldt Kids y corrige datos de admisiones
```

Árbol limpio. **Nada de esto está en producción todavía.**

- **Preview pública:** https://humboldt-admisiones-aaupva8p4-musiclimpics.vercel.app
  (cada `vercel --yes` crea una URL nueva; para la vigente, `vercel ls`)
- **Producción:** https://humboldt-admisiones.vercel.app — sirve la versión vieja de `main`
- **Repo:** https://github.com/alcolhumboldt-byte/humboldt-admisiones

La protección SSO de Vercel se desactivó para que la preview sea compartible.
Aplica a **todo el proyecto**, no solo a un despliegue. Para revertirla:
`vercel project protection enable --sso`

## Stack
- Estático puro. Un solo `index.html` con CSS y JS inline. Sin build.
- Despliegue: Vercel. Sin build step.
- Fuentes: Google Fonts. **Archivo** (display), **Source Sans 3** (texto),
  **Shantell Sans** (una sola palabra del hero), **Fredoka** (solo Humboldt Kids).

## Dirección de diseño

La página es **clara siempre**. No sigue el tema del sistema; el modo oscuro
se eliminó por decisión del colegio. Estaba resuelto y verificado en AA en el
commit `3542f7f` si algún día se quiere recuperar.

Reglas que hay que respetar al editar:

- **La fotografía es el diseño.** Sin fotos reales la página no funciona.
  Es la tarea número uno, por encima de cualquier ajuste visual.
- **Titulares en caja mixta**, no versalitas. El bloque de mayúsculas
  endurecía la página. El gesto lo da la manuscrita de acento.
- **La manuscrita (Shantell Sans) aparece una sola vez**, en "abiertas" del
  hero. Si se repite deja de ser gesto y se vuelve decoración.
- **El índigo `#211C6C` es el color dominante**: campos completos (banda de
  cifras, laboratorios, footer, cierre de Humboldt Kids). No es un acento
  diluido sobre cada elemento.
- **Un solo sistema de esquinas: radio 0.** Las dos excepciones son el botón
  flotante de WhatsApp y todo lo que vive dentro de `.hk`.
- **Presupuesto de rótulos: 3 en toda la página** (hero, laboratorios,
  contacto). Ponerlo en cada sección es la firma más reconocible de página
  hecha por IA. Si agregas una sección, no le pongas rótulo.
- **Sin rayas em ni en (`—`, `–`) en ningún texto visible.** Coma, punto o
  dos puntos. Es la otra firma delatora.
- **El texto se gana su lugar.** Titulares de 8 palabras o menos, párrafos de
  25 o menos. El titular del hero es de 2 líneas en escritorio: regla dura.
- **Familias de layout, una vez cada una.** No repetir una familia en dos
  secciones.

## Paleta

| Token | Valor | Uso |
|---|---|---|
| `--tinta` / `--marca-txt` | `#211C6C` | Índigo del logo. Fondos y titulares de marca |
| `--tinta-hover` | `#171248` | El mismo, al pasar el puntero |
| `--morado` | `#6D68B0` | Morado medio del logo |
| `--lavanda` | `#B7B3E3` | Lavanda del logo. "abiertas" en el hero |
| `--amarillo` | `#F5B700` | Preescolar. Coincide con el dorado de la mascota |
| `--turquesa` | `#00B4A6` | Primaria |
| `--coral` | `#FF5A5F` | Secundaria |
| `--violeta` | `#7B61FF` | Media |

**Cada acento tiene un par `-txt` más oscuro.** Los tonos plenos no alcanzan
4.5:1 sobre papel. Para fondos y figuras se usa el pleno; para texto sobre
claro, el `-txt`. Romper esto rompe el contraste AA, que está verificado en
toda la página.

## Estructura

1. Nav sticky, 5 anclas y CTA. Colapsa a hamburguesa bajo 1020px.
2. Hero: foto a sangre, titular "Admisiones abiertas", CTA WhatsApp
3. Banda de 3 cifras sobre índigo
4. `#formacion` — rejilla asimétrica de 3 tarjetas foto
5. `#niveles` — lista rayada de 4 filas, cada una con su marca geométrica y
   su color. La mascota preside la sección.
6. `#humboldt-kids` — **mundo visual propio**, ver abajo
7. `#laboratorios` — declaración grande sobre campo índigo
8. `#instalaciones` — dos listas rayadas, bloque de logro, mosaico de fotos
9. `#admision` — 3 pasos numerados + panel de horarios en relieve
10. `#contacto` — CTA WhatsApp, datos, mapa, formulario de 3 campos
11. `#faq` — acordeón
12. Footer índigo + botón WhatsApp flotante

Nota: el nav lista 5 secciones. Al agregar otra, quitar una antes.

## Humboldt Kids

Sección para Preescolar y Primaria con estética propia: dorado de fondo,
curvas, Fredoka redonda, título con contorno tipo calcomanía, sombras
sólidas desplazadas.

**Todo su estilo vive bajo `.hk`.** Esa encapsulación es deliberada: evita
que la estética infantil se filtre al resto de la página, que le habla a un
papá de 11°. No sacar reglas de `.hk` al ámbito global.

Usa ilustraciones de undraw en `ilustraciones/`, ya en el índigo del logo.

## Convenciones del código

- Todo elemento con clase `.wa` recibe el link de WhatsApp automáticamente.
  El texto prellenado sale de `data-msg`. Para un CTA nuevo:
  `<a href="#" class="wa" data-msg="...">`
- Variables CSS en `:root`. No hardcodear colores.
- `.rv` = aparición al hacer scroll (IntersectionObserver). `.cascada` en el
  contenedor escalona los hijos.
- El nav usa **centinela de 1px + IntersectionObserver**, no un listener de
  `scroll`: ese listener corre en cada frame y el navegador no lo batchea.
- **Animación:** `--ease-out` para entradas y salidas, `--ease` para hover y
  color. Pulsación a 160ms. Todo `:hover` va dentro de
  `@media (hover: hover) and (pointer: fine)` para que no se dispare al tocar
  en móvil. `prefers-reduced-motion` detiene los bucles infinitos por
  completo, no los acorta.
- **Relieve:** tokens `--neu-alto`, `--neu-bajo`, `--neu-hundido`. Solo en
  contenedores (horarios, FAQ, inputs). El contraste del texto nunca depende
  de esas sombras, y los inputs conservan su borde.
- **Respaldo de imágenes:** cada `<img>` apunta a su archivo real y cae a
  `picsum` vía `data-respaldo`. Si ambas fallan, la imagen se **oculta** en
  vez de dibujar su texto alternativo, que dice "[ PLACEHOLDER ]". El
  listener de error **no** puede llevar `{ once: true }`: hacen falta dos
  fallos, el de la foto real y el del respaldo.
- Marcadores `[ ... ]` = contenido pendiente por reemplazar.

## Tareas pendientes

### Bloqueantes para lanzar

1. **Las 14 fotos.** Hoy todas caen a `picsum`, que son fotos de stock de
   gente ajena al colegio. Buscar `TODO FOTO` en el HTML; las medidas y los
   nombres exactos están en `fotos/LEEME.md`. **Ninguna puede salir a
   producción.** Hay autorización de imagen de por medio: son menores.
2. **FAQ, 2 respuestas:** requisitos de 9°, 10° y 11°, y política de ingreso
   a mitad de año. Están marcadas con `[ ... ]` y son visibles en la página.
3. **Año escolar del hero.** El rótulo dice "Prejardín a grado 11", que
   duplica la banda de cifras justo debajo. Se decidió cambiarlo por el año
   ("Año escolar 2027") pero falta confirmar cuál es.
4. **Fusionar `humboldt-kids` a `main` y desplegar a producción.**

### Después del lanzamiento

- `const ENDPOINT`: hoy vacío, así que el formulario abre WhatsApp con los
  datos prellenados. Sin correo de admisiones, ese es el comportamiento
  definitivo, no un respaldo. **Ojo:** el texto de contacto dice "déjanos tus
  datos y te contactamos", pero si el acudiente no pulsa enviar en WhatsApp,
  ese lead no existe para nadie. O se ajusta el texto, o se conecta el
  endpoint a una tabla en Supabase.
- SEO: `og:image`, favicon, JSON-LD tipo `School`. Importa más de lo normal
  porque el canal de distribución es WhatsApp: cuando alguien reenvía el
  link, la tarjeta de vista previa es lo que se comparte.
- Autoalojar las fuentes. Hoy son 4 familias por `<link>` a Google Fonts.
- Pixel de Meta para pauta pagada.
- Testimonios reales de padres.

## Datos del colegio

- **Dirección:** Calle 3 #7a-45, Sogamoso, Boyacá
- **WhatsApp:** 320 458 1513 — es el número que responde chats
- **Llamadas:** 310 875 2661 — **no** responde WhatsApp
- **Fijo:** 770 04 94
- **Sin correo de admisiones.** Todo va por WhatsApp, por decisión del colegio.
- **Formulario de inscripción:** $70.000, dos partes, una la diligencia el
  acudiente y otra el colegio actual del estudiante
- **Horarios:** Preescolar 7:15 a 12:45, primaria 6:45 a 12:45, secundaria y
  media 6:15 a 1:30. Lúdicas 2 o 3 días, no obligatorias.
- **ICFES:** 2° en la ciudad, entre los cinco mejores los últimos años. Es el
  puesto **del colegio**, no de estudiantes sueltos.
- Costos de matrícula y pensión los regula la Secretaría de Educación.

## Decisiones ya tomadas, no rediscutir

- WhatsApp es la acción principal, no el formulario.
- El área de tecnología se vende como **Laboratorios de Química e Innovación**,
  nunca como "clase de sistemas". Se vende el método, no el producto.
- Sin CMS. El contenido se edita directo en el HTML.
- Nombre oficial: **Colegio Alejandro de Humboldt**, con "de".
- La página es siempre clara. Sin modo oscuro.
- El tercer pilar de formación se llama **Formación en valores cristianos**.

## Advertencias

- **La mascota fue recoloreada.** Su navy original era `#00243C`, que choca
  con el índigo del logo. Se llevó a `#211C6C`. Si el colegio la usa impresa
  en el navy original, hay dos versiones circulando: vale confirmarlo.
- **El infográfico de inscripción está vencido.** Dice "valores para el 2025"
  y estamos en agosto de 2026. Confirmar que el proceso sigue igual.
- **Definir quién responde el WhatsApp y en qué horario antes de lanzar.**
  Un lead sin respuesta en menos de 5 minutos se enfría. Sin eso la página no
  sirve por buena que quede.
- **Nada de lo que está en `[ ... ]` puede salir a producción.**
- El panel de vista previa del entorno de desarrollo no sincroniza bien el
  scroll ni el caché. Verificar con recarga forzada (`?v=N`) y, ante la duda,
  comprobar por JS en vez de fiarse de la captura.
