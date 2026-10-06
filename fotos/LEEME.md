# Fotos del colegio

Aquí van las 38 fotos de la landing. **Los nombres tienen que ser exactos**: el HTML ya apunta a ellos. No hay que tocar código, solo dejar los archivos en esta carpeta.

Mientras un archivo no exista, la página muestra en su lugar una foto de relleno de `picsum.photos`. Apenas dejes el archivo real con el nombre correcto, aparece solo.

## Los 38 archivos

| Archivo | Dónde sale | Medida | Estado |
|---|---|---|---|
| `01-hero.jpg` | Portada, pantalla completa | 2400 × 1400 | listo |
| `04-formacion-caracter.jpg` | Formación, tarjeta grande | 1600 × 900 | listo |
| `03-rigor-academico.jpg` | Formación, tarjeta 02 | 1200 × 900 | listo |
| `02-investigacion-desarrollo.jpg` | Formación, tarjeta 03 | 1200 × 900 | listo |
| `05-patio-central.jpg` | Mosaico, celda grande | 1600 × 1600 | listo |
| `06-sala-computo.jpg` | Mosaico | 900 × 900 | listo |
| `07-acompanamiento.jpg` | Mosaico | 900 × 900 | listo |
| `08-biblioteca.jpg` | Mosaico | 900 × 900 | listo |
| `09-preescolar.jpg` | Mosaico | 900 × 900 | listo |
| `10-deportes.jpg` | Mosaico, celda ancha | 1800 × 900 | listo |
| `11-juego-libre.jpg` | Mosaico | 900 × 900 | listo |
| `12-vida-escolar.jpg` | Mosaico | 900 × 900 | listo |
| `15-laboratorio.jpg` | Mosaico | 900 × 900 | listo |
| `16-clase.jpg` | Mosaico | 900 × 900 | listo |
| `17-parvulos.jpg` | Mosaico | 900 × 900 | listo |
| `18-piano.jpg` | Mosaico | 900 × 900 | listo |
| `19-canchas.jpg` | Mosaico, instalación | 900 × 900 | listo |
| `20-sala-lectura.jpg` | Mosaico, instalación | 900 × 900 | listo |
| `21-corredor.jpg` | Mosaico, instalación | 900 × 900 | listo |
| `22-zona-verde.jpg` | Mosaico, instalación | 900 × 900 | listo |
| `13-sala-multiple.jpg` | Humboldt Kids | 1600 × 1000 | listo |
| `14-salon-musica.jpg` | Humboldt Kids | 1600 × 1000 | listo |

Los originales están en `~/Desktop/fotos humboldt/` y `~/Desktop/REDES/`. Se recortaron al centro
según la proporción de cada slot y se comprimieron por debajo de 300 KB.

**Las 38 están montadas.** Ya no hay huecos con imágenes de stock.

El mosaico arranca colapsado mostrando **8 de 16**, y las instalaciones van
de primeras para que se vean sin pulsar el botón. Tiene **32 celdas exactas**. La rejilla cierra cada 4 celdas: 12, 16, 20, 24, 28, 32. Con otro número queda coja. Los tramos anchos son la 1 (2x2) y la
6 (2x1), que es donde va la foto de deportes, la única en 1800x900; si cambias el número de fotos hay que recalcularlos o la retícula
queda con huecos.

Las dos últimas son de la sección Humboldt Kids. Ahí importa más que en
ninguna otra parte que salgan **niños en actividad**, no el salón vacío:
esa sección existe para que un papá imagine a su hijo adentro.

## Qué foto sirve y cuál no

La página está construida sobre la fotografía: si las fotos son flojas, no la salva ningún ajuste de diseño.

Las cuatro últimas del mosaico son instalaciones sin gente, a propósito: un
acudiente que aún no ha visitado quiere ver la planta física. Son el
complemento, no el grueso. El resto de la galería son estudiantes en
actividad, y esa proporción no debería invertirse.

- **Gente, no salones vacíos.** Una biblioteca sin nadie es un cuarto con libros. Con tres estudiantes leyendo es el colegio.
- **Estudiantes haciendo algo**, no posando en fila mirando a la cámara.
- **Horizontal para las cuatro primeras.** Si las mandan verticales, el recorte va a cortar cabezas.
- **Luz de día.** Nada de flash directo ni salones a media luz.
- **Sin marca de agua, sin fecha impresa, sin collages.** Una foto por archivo.
- La `01-hero.jpg` es la más importante: es lo primero que ve el acudiente y ocupa toda la pantalla. Que se lea claro qué está pasando incluso en miniatura.

## Antes de subirlas

Bajar el peso. Una foto de celular puede pesar 5 MB y la página tiene 12: así entraría lentísima en datos móviles, que es como la va a abrir la mayoría de acudientes.

- Meta: **menos de 300 KB por foto**.
- Herramienta sin instalar nada: <https://squoosh.app> (arrastrar, elegir calidad ~75, descargar).
- Formato: `.jpg`. Si la herramienta ofrece `.webp` y la usas, hay que cambiar la extensión en el HTML.

## Permisos

Son menores de edad. Antes de publicar, confirmar con el colegio que hay **autorización de uso de imagen firmada por los acudientes** de cada estudiante que salga identificable. Es requisito legal, no un trámite opcional.

## Cuando estén las 12

Borrar del `<script>` de `index.html` el bloque comentado `---- Respaldo de imágenes ----` y los atributos `data-respaldo` de los `<img>`. Ya no hacen falta y evitan que un error de nombre pase inadvertido mostrando una foto de stock en producción.
