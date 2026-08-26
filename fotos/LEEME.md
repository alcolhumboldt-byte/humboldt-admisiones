# Fotos del colegio

Aquí van las 12 fotos de la landing. **Los nombres tienen que ser exactos**: el HTML ya apunta a ellos. No hay que tocar código, solo dejar los archivos en esta carpeta.

Mientras un archivo no exista, la página muestra en su lugar una foto de relleno de `picsum.photos`. Apenas dejes el archivo real con el nombre correcto, aparece solo.

## Los 12 archivos

| Archivo | Dónde sale | Medida mínima | Forma |
|---|---|---|---|
| `01-hero.jpg` | Portada, a pantalla completa | 2400 × 1400 | horizontal |
| `02-investigacion-desarrollo.jpg` | Formación, tarjeta grande | 1600 × 900 | horizontal |
| `03-rigor-academico.jpg` | Formación, tarjeta 02 | 1200 × 900 | horizontal |
| `04-formacion-caracter.jpg` | Formación, tarjeta 03 | 1200 × 900 | horizontal |
| `05-patio-central.jpg` | Mosaico, celda grande | 1600 × 1600 | cuadrada |
| `06-laboratorio-quimica.jpg` | Mosaico | 900 × 900 | cuadrada |
| `07-aula-musica.jpg` | Mosaico | 900 × 900 | cuadrada |
| `08-biblioteca.jpg` | Mosaico | 900 × 900 | cuadrada |
| `09-sala-informatica.jpg` | Mosaico | 900 × 900 | cuadrada |
| `10-deportes.jpg` | Mosaico, celda ancha | 1800 × 900 | horizontal 2:1 |
| `11-clase-ingles.jpg` | Mosaico | 900 × 900 | cuadrada |
| `12-vida-escolar.jpg` | Mosaico | 900 × 900 | cuadrada |

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
