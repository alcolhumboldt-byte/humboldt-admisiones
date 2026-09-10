# Fotos del colegio

Aquí van las 14 fotos de la landing. **Los nombres tienen que ser exactos**: el HTML ya apunta a ellos. No hay que tocar código, solo dejar los archivos en esta carpeta.

Mientras un archivo no exista, la página muestra en su lugar una foto de relleno de `picsum.photos`. Apenas dejes el archivo real con el nombre correcto, aparece solo.

## Los 14 archivos

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
| `13-sala-multiple.jpg` | Humboldt Kids | 1600 × 1000 | listo |
| `14-salon-musica.jpg` | Humboldt Kids | 1600 × 1000 | listo |

Los originales están en `~/Desktop/fotos humboldt/`. Se recortaron al centro
según la proporción de cada slot y se comprimieron por debajo de 300 KB.

**Las 14 están montadas.** Ya no hay huecos con imágenes de stock.

Las dos últimas son de la sección Humboldt Kids. Ahí importa más que en
ninguna otra parte que salgan **niños en actividad**, no el salón vacío:
esa sección existe para que un papá imagine a su hijo adentro.

## Qué foto sirve y cuál no

La página está construida sobre la fotografía: si las fotos son flojas, no la salva ningún ajuste de diseño.

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
