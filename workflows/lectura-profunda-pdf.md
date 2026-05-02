# Lectura Profunda de Libros (PDF / EPUB / formatos largos)

Workflow para cuando el usuario pide leer un libro completo (no solo evaluar metadatos), garantizando una lectura sustantiva sin caer en limites de la herramienta `Read`.

Usar este workflow cuando el usuario pida algo como: *"leelo completo"*, *"haz una pasada real por los capitulos"*, *"no te saltes el cuerpo del libro"*, *"que has omitido del libro?"*. Tambien cuando una evaluacion previa se hizo solo sobre prologo/contraportada/bibliografia y se necesita verificar la tesis con el contenido real.

---

## Por Que Este Workflow Existe

`Read` sobre un PDF renderiza cada pagina como imagen y la inyecta en el contexto del modelo. Un libro largo o con imagenes de alta resolucion satura el limite de 32MB por request y aborta con error: `Request too large (max 32MB)`. Reducir el rango de paginas no siempre alcanza si el PDF tiene fotografia en alta resolucion (libros etnograficos, arte, arqueologia).

La solucion es separar dos preocupaciones:

1. **Extraer el texto** con `pdftotext` (no renderiza imagenes, salida en KB no MB).
2. **Razonar sobre el texto** con `Read` sobre el `.txt` extraido (sin limite practico).

Asi se conserva la riqueza analitica de leer el cuerpo del libro sin perder paginas por error de tamano.

---

## Paso 0: Triaje del Archivo

Antes de leer nada, identificar tres datos clave:

```bash
pdfinfo "<ruta-del-pdf>"
```

De ahi obtener: paginas totales, autor segun metadata, tamano del archivo.

Verificar tambien:

- Carpeta padre (puede revelar atribucion sospechosa, ej: Calibre con autor incorrecto).
- Existencia de `metadata.opf`, `cover.jpg`, archivos hermanos.

Si la metadata del PDF y la carpeta del usuario discrepan en autor o titulo, sospechar y advertir antes de continuar. La portada y la pagina de derechos del PDF mandan, no Calibre.

---

## Paso 1: Extraer la Tabla de Contenidos

```bash
pdftotext -f 1 -l 20 -layout "<pdf>" /tmp/<libro>_toc.txt
```

Leer ese `.txt`. Identificar:

- Estructura de capitulos y rangos de paginas.
- Si el libro es bilingue (ES/EN, FR/EN): el contenido neto es la mitad y los rangos se duplican.
- Apendices, glosarios, indices analiticos al final (paginas a leer aparte).

Si no hay indice impreso, abrir `pdftotext -f 1 -l 5 -layout` y mirar como esta numerado. Algunos libros tienen numeracion romana en preliminares + arabiga desde el cap.1.

---

## Paso 2: Plan de Bloques

Dividir el libro en bloques de **15-20 paginas maximo** (no mas). Razones:

- Cada bloque cabe holgado en `Read` aun con `pdftotext` raro o muy denso.
- Bloques chicos permiten emitir notas inmediatas tras cada lectura, evitando saturar contexto.
- Si un bloque falla (formato extrano, tablas grandes), se reduce a 10 paginas sin reiniciar.

Estructura recomendada:

| Bloque | Paginas tipicas | Foco |
|---|---|---|
| 0 | Prologo + Indice + Agradecimientos | Tesis declarada, informantes, dedicatoria |
| 1..N | Capitulos | Cuerpo argumental |
| N+1 | Reflexiones finales / Conclusiones | Cierre de tesis, comparaciones |
| N+2 | Bibliografia + Anexos + Indice | Verificacion de fuentes |

---

## Paso 3: Bucle de Lectura por Bloque

Para cada bloque:

```bash
pdftotext -f <ini> -l <fin> -layout "<pdf>" /tmp/<libro>_<ini>_<fin>.txt
```

Luego `Read` sobre el `.txt`. Inmediatamente despues, **emitir una nota corta al usuario** con los 5-10 hallazgos del bloque: hechos, citas con pagina, conceptos, nombres propios, datos verificables. No esperar al final del libro para sintetizar.

Razones para emitir nota tras cada bloque:

- El usuario puede corregir el rumbo si la lectura se desvia.
- Si la sesion se interrumpe, el trabajo hasta ese punto esta consolidado en el chat.
- Reduce el riesgo de olvido por compresion de contexto en sesiones largas.

Mantener cada nota de bloque por debajo de 200 palabras. La sintesis profunda viene al final, no en cada bloque.

---

## Paso 4: Estrategias para Casos Dificiles

### El bloque sigue siendo demasiado grande

Si `pdftotext` produce un `.txt` mayor de ~500 KB (raro pero posible con OCR malo), reducir a bloques de 10 paginas. Si aun asi falla, el PDF probablemente esta escaneado sin OCR aplicado: ejecutar OCR antes de continuar:

```bash
ocrmypdf "<pdf-original>" "<pdf-ocr>"
```

Y volver al Paso 1 con el PDF nuevo.

### Layout en multiples columnas

`-layout` preserva columnas pero a veces mezcla parrafos. Probar sin `-layout`:

```bash
pdftotext -f <ini> -l <fin> "<pdf>" /tmp/out.txt
```

Si tampoco, usar `-raw`. Comparar los tres y elegir el mas legible.

### Libros bilingues

El texto extraido alterna idiomas. Filtrar mentalmente o, si estorba, extraer por columnas con `pdftotext -layout` y procesar la columna del idioma deseado.

### Notas al pie y citas

`pdftotext` mezcla notas al pie con el cuerpo. Cuando una cita relevante aparece, anotar su pagina exacta del PDF (no la pagina impresa, que puede diferir) para poder volver a verificar.

### EPUB en lugar de PDF

```bash
pandoc "<libro.epub>" -t plain -o /tmp/<libro>.txt
```

El EPUB ya es texto, no tiene este problema. Procesar con la misma logica de bloques.

### TXT plano

Si el archivo ya es `.txt`, `Read` directo con `offset` y `limit` por bloques de 1500-2000 lineas.

---

## Paso 5: Sintesis Final

Una vez leidos todos los bloques, integrar las notas en una evaluacion completa siguiendo `evaluar-despues-de-leer.md`. La diferencia respecto a una evaluacion sin lectura profunda:

- Las dimensiones **Profundidad**, **Balance** y **Vigencia** ahora se sostienen en lectura directa, no en inferencia desde la presentacion.
- La verificacion de claims (Paso 3 del workflow post-lectura) puede usar las paginas exactas anotadas en cada bloque.
- Las citas textuales se pueden reproducir literalmente, no parafrasear.

Si el libro merece notas duraderas (ej: vault de Obsidian del usuario), separar:

- Una nota de **referencia/evaluacion** (fichada, citas con pagina, puntuacion).
- Una nota de **inspiracion/extraccion** (semillas creativas, imagineria, arquetipos).

Ver `templates/rubrica-puntuacion.md` para la primera. La segunda no usa plantilla fija: se organiza por nucleos tematicos del libro.

---

## Limpieza

Los archivos `/tmp/<libro>_*.txt` se pueden conservar mientras dure la sesion. Son utiles si el usuario pide revisar un bloque ya leido sin re-extraer. Si la sesion termina y no se quiere dejar residuos:

```bash
rm /tmp/<libro>_*.txt
```

No borrar antes de terminar la sintesis final.

---

## Senales de que NO Conviene Lectura Profunda

Este workflow tiene costo en tiempo y contexto. Saltarlo si:

- El usuario solo quiere decidir si comprar el libro (usar `evaluar-antes-de-comprar.md`).
- El libro es de autoayuda con bibliografia minima (la lectura profunda no rescata calidad inexistente).
- El usuario explicita "evaluacion rapida" o "no hace falta leerlo entero".
- El libro ya tiene resena confiable de un experto del campo y el usuario solo quiere segunda opinion.

En esos casos, una evaluacion estructural (autoridad + bibliografia + indice + 2-3 capitulos sample) es mas eficiente.
