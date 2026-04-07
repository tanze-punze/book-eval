---
name: book-eval
description: >
  Rubrica sintetizada y frameworks para evaluar libros de no ficcion: credibilidad del autor,
  precision de datos, profundidad del analisis, utilidad practica. Basada en CRAAP Test, SIFT,
  criterios Thwink.org, NCTE Orbis Pictus y sistema academico espanol (SPI/ANECA).
  USE WHEN el usuario quiere evaluar un libro de no ficcion, decidir si comprar un libro,
  analizar la calidad de un libro, verificar si un libro es confiable, evaluar la credibilidad
  de un autor, comparar libros de no ficcion, revisar un libro de autoayuda, verificar fuentes
  de un libro, obtener una rubrica de evaluacion de libros, o cualquier analisis critico de
  literatura no ficcion. Tambien aplica si piden "vale la pena leer X", "es bueno este libro",
  "que tan confiable es", "deberia comprar este libro", o si necesitan criterios de calidad
  editorial. NO aplica para ficcion, novelas, poesia, ni resenas literarias de estilo/narrativa.
---

# Evaluador de Libros de No Ficcion

Skill para evaluar libros de no ficcion con rigor critico. Proporciona frameworks, rubricas,
workflows y checklists para determinar si un libro es confiable y su informacion realmente util.

**Dato clave:** Los libros NO pasan por fact-checking sistematico como las revistas academicas.
La responsabilidad de verificar recae en el lector. Incluso autores famosos distorsionan datos
(ej: Gladwell y la "regla de las 10,000 horas" que malinterpreto los datos originales de Ericsson).

---

## Como Usar Esta Skill

| Necesitas... | Lee este archivo |
|---|---|
| Evaluacion rapida (checklists) | `checklists/checklist-rapido.md` |
| Decidir si comprar un libro | `workflows/evaluar-antes-de-comprar.md` |
| Evaluar mientras lees | `workflows/evaluar-mientras-lees.md` |
| Evaluacion completa post-lectura | `workflows/evaluar-despues-de-leer.md` |
| Plantilla de puntuacion rellenable | `templates/rubrica-puntuacion.md` |
| Framework CRAAP (el mas usado) | `references/01-craap-test.md` |
| Metodo SIFT (evaluacion rapida) | `references/02-sift-method.md` |
| Criterios Thwink (calidad argumental) | `references/03-thwink-criteria.md` |
| Criterios NCTE Orbis Pictus | `references/04-orbis-pictus-ncte.md` |
| Sistema academico espanol | `references/05-sistema-academico-espanol.md` |
| Banderas rojas por categoria | `references/06-banderas-rojas.md` |

---

## Mapa de Decisiones

```
Quieres decidir si COMPRAR un libro?
  --> Evaluacion rapida en 10-15 minutos
  --> workflows/evaluar-antes-de-comprar.md

Estas LEYENDO un libro y quieres evaluar sobre la marcha?
  --> Evaluacion progresiva por capitulos
  --> workflows/evaluar-mientras-lees.md

Ya TERMINASTE el libro y quieres una evaluacion completa?
  --> Rubrica completa con puntuacion
  --> workflows/evaluar-despues-de-leer.md + templates/rubrica-puntuacion.md

Es un libro de AUTOAYUDA / desarrollo personal?
  --> Escrutinio extra: verificar formacion profesional del autor
  --> references/06-banderas-rojas.md (seccion Autoayuda)

Necesitas evaluar con criterios ACADEMICOS (tesis, publicacion)?
  --> Sistema SPI/ANECA/CEA-APQ
  --> references/05-sistema-academico-espanol.md

Solo quieres la RUBRICA para puntuar?
  --> templates/rubrica-puntuacion.md (9 dimensiones, escala 1-5)

Quieres entender un FRAMEWORK especifico?
  --> references/01-craap-test.md a references/04-orbis-pictus-ncte.md
```

---

## Rubrica Sintetizada -- Referencia Rapida

Rubrica de 9 dimensiones sintetizada a partir de CRAAP Test, SIFT, Thwink, NCTE y sistema
academico espanol. Para la plantilla rellenable completa ver `templates/rubrica-puntuacion.md`.

| Dimension | Peso | Que evaluar | Indicadores positivos | Indicadores negativos |
|---|---|---|---|---|
| **Autoridad** | ALTO (x3) | Credenciales, formacion, trayectoria del autor | PhD/maestria relevante, publicaciones peer-reviewed, experiencia profesional demostrable, afiliacion institucional | Sin biografia, credenciales no verificables, solo "coach certificado" sin especificar por quien |
| **Precision** | ALTO (x3) | Citas, bibliografia, fuentes verificables | Bibliografia extensa, citas con pagina/DOI, datos con fuente primaria, notas al pie rigurosas | Sin citas, datos sin fuente, "estudios demuestran que..." sin especificar cuales |
| **Profundidad** | ALTO (x3) | Mas alla de lo superficial, causas raiz | Aborda complejidad, reconoce limitaciones, multiples perspectivas, analisis de causas | Simplifica en exceso, soluciones magicas, ignora contraejemplos, superficial |
| **Utilidad practica** | ALTO (x3) | Proceso accionable, aprendizaje real | Frameworks aplicables, ejercicios, casos de estudio reales, metodologia replicable | Solo teoria sin aplicacion, promesas vacias, consejos genericos |
| **Estructura** | MEDIO (x2) | Organizacion logica, progresion clara | Indice detallado, glosario, progresion logica, cada capitulo aporta algo nuevo | Repetitivo, desorganizado, sin hilo conductor, relleno |
| **Balance** | MEDIO (x2) | Perspectivas multiples, contraargumentos | Presenta criticas a su propia posicion, cita detractores, reconoce incertidumbre | Solo una narrativa, ignora evidencia contraria, sesgo de confirmacion |
| **Vigencia** | MEDIO (x2) | Actualidad de datos y fuentes | Fuentes <5 anos, ediciones actualizadas, datos vigentes para el campo | Datos obsoletos, campo evoluciono significativamente desde la publicacion |
| **Escritura** | MEDIO (x2) | Claridad, precision del lenguaje | Clara sin ser simplista, jerga explicada, tono equilibrado entre rigor y accesibilidad | Retorica emocional excesiva, relleno, vaguedad, jerga sin explicar |
| **Respaldo editorial** | MEDIO-BAJO (x1) | Editorial, proceso de revision | Editorial con reputacion, coleccion especializada, proceso editorial visible | Autopublicado sin revision, editorial vanity press, sin proceso editorial |

---

## Sistema de Puntuacion

**Escala:** 1 a 5 por dimension (1=muy deficiente, 5=excelente)

**Formula ponderada:**

```
Puntuacion = (Autoridad*3 + Precision*3 + Profundidad*3 + Utilidad*3 +
              Estructura*2 + Balance*2 + Vigencia*2 + Escritura*2 +
              Editorial*1) / 21
```

**Interpretacion:**

| Rango | Categoria | Significado |
|---|---|---|
| 4.5 - 5.0 | Excelente | Lectura esencial en su campo |
| 3.5 - 4.4 | Bueno | Vale la pena leer |
| 2.5 - 3.4 | Regular | Tiene valor parcial, leer con precaucion critica |
| 1.5 - 2.4 | Pobre | Problemas significativos de confiabilidad o utilidad |
| 1.0 - 1.4 | Evitar | Informacion poco confiable, no recomendado |

---

## Banderas Rojas -- Deteccion Rapida

Para el catalogo completo de banderas rojas por categoria, ver `references/06-banderas-rojas.md`.

**CRITICO** (cualquiera de estos = precaucion maxima):

- Sin bibliografia ni referencias de ningun tipo
- Credenciales del autor no verificables en ninguna fuente externa
- Promesas excesivas ("cambiara tu vida", "el unico metodo que funciona")
- Solo anecdotas personales como evidencia, cero datos verificables

**SERIO** (2+ de estos = evaluar con cuidado):

- Contenido repetitivo / relleno evidente
- Retorica emocional sustituyendo evidencia logica
- Autopublicado sin proceso de revision editorial visible
- Sin indice tematico, glosario ni notas

**CONTEXTUAL** (depende del campo y tipo de libro):

- Autoayuda escrita por autor sin formacion profesional en psicologia/terapia
- Ciencia popular escrita por periodistas sin citar fuentes primarias
- Datos de mas de 5 anos en campos de rapida evolucion (tecnologia, medicina, IA)
- Negocios/emprendimiento con sesgo de supervivencia no reconocido

---

## Frameworks en una Mirada

### CRAAP Test (el mas utilizado)
Desarrollado por Sarah Blakeslee en CSU Chico. Evalua 5 dimensiones: Currency (vigencia),
Relevance (relevancia), Authority (autoridad), Accuracy (precision), Purpose (proposito).
Es el framework de referencia en bibliotecas academicas de todo el mundo.
Detalle completo: `references/01-craap-test.md`

### Metodo SIFT
Creado por Mike Caulfield para alfabetizacion digital. 4 pasos procedimentales: Stop (detenerse),
Investigate the source (investigar la fuente), Find better coverage (buscar mejor cobertura),
Trace claims (rastrear afirmaciones hasta su origen). Ideal para evaluacion rapida antes de comprar.
Detalle completo: `references/02-sift-method.md`

### 7 Criterios de Thwink (Jack Harich)
Enfocado en la calidad intelectual del contenido: claridad del argumento, regla 80/20, profundidad
de analisis, causas raiz vs sintomas, calidad de evidencia, consideracion de contraargumentos,
aplicabilidad practica. Complementa al CRAAP porque evalua el argumento, no solo la fuente.
Detalle completo: `references/03-thwink-criteria.md`

### NCTE / Orbis Pictus
Criterios del National Council of Teachers of English para excelencia en no ficcion: precision,
organizacion, estilo de escritura, diseno, documentacion de fuentes. Originalmente para no ficcion
educativa pero aplicable a cualquier no ficcion que busque ser rigurosa y accesible.
Detalle completo: `references/04-orbis-pictus-ncte.md`

### Sistema Academico Espanol (SPI/ANECA/CEA-APQ)
Indicadores de calidad editorial del sistema academico hispanohablante: Scholarly Publishers
Indicators (SPI), sello de Calidad en Edicion Academica (CEA-APQ), criterios ANECA/CNEAI.
Usar cuando se evaluan publicaciones academicas o editoriales universitarias.
Detalle completo: `references/05-sistema-academico-espanol.md`

---

## Ejemplo de Evaluacion Rapida

**Libro:** "Sapiens: De animales a dioses" - Yuval Noah Harari (2014)

| Dimension | Punt. | Nota rapida |
|---|---|---|
| Autoridad | 4 | PhD en Historia (Oxford), profesor en Hebrew University. Historiador, no biologo ni antropologo para algunos temas que aborda |
| Precision | 3 | Bibliografia presente pero algunas afirmaciones son generalizaciones amplias dificiles de verificar. Criticas academicas documentadas sobre simplificaciones |
| Profundidad | 4 | Abarca 70,000 anos con narrativa ambiciosa. Profundo en vision macro, a veces superficial en detalles |
| Utilidad | 3 | Cambia perspectiva sobre la historia humana pero pocas herramientas accionables directas |
| Estructura | 5 | Progresion logica clara: cognitiva -> agricola -> unificacion -> cientifica |
| Balance | 3 | Presenta su narrativa con conviccion, algunos contraargumentos pero tiende a una tesis dominante |
| Vigencia | 4 | Historia antigua no caduca, pero algunas proyecciones sobre IA/biotecnologia ya estan fechadas |
| Escritura | 5 | Prosa excepcional, accesible sin ser simplista, mantiene el enganche |
| Editorial | 5 | Harper/Debate, editorial de primera linea, multiples ediciones y traducciones |

**Puntuacion:** (4x3 + 3x3 + 4x3 + 3x3 + 5x2 + 3x2 + 4x2 + 5x2 + 5x1) / 21 = **3.86 (Bueno)**

**Veredicto:** Vale la pena leer como vision panoramica de la historia humana, pero no como
fuente academica precisa en temas especificos. Leer con conciencia de que es una narrativa
interpretativa, no un textbook.

---

## Por Que Existe Esta Skill

A diferencia de las revistas academicas con revision por pares y fact-checking sistematico,
los libros pasan por procesos editoriales minimos de verificacion de datos. Como senala la
investigacion sobre la industria editorial: "la verificacion de datos nunca ha sido una practica
estandar en la industria editorial de libros."

Esto significa que:
- Bestsellers pueden contener errores factuales significativos
- La fama del autor no garantiza precision
- La calidad editorial (buena prosa, buen diseno) no implica rigor informativo
- El lector necesita herramientas propias para evaluar criticamente

Esta skill proporciona esas herramientas de evaluacion critica. La decision final de lectura
o compra es siempre del usuario.

---

## Fuentes de los Frameworks

- **CRAAP Test:** Sarah Blakeslee, Meriam Library, California State University, Chico (2004)
- **SIFT Method:** Mike Caulfield, "Web Literacy for Student Fact-Checkers" (2019)
- **7 Criterios Thwink:** Jack Harich, thwink.org
- **Orbis Pictus / NCTE:** National Council of Teachers of English
- **SPI:** Scholarly Publishers Indicators, CSIC (Espana)
- **CEA-APQ:** Sello de Calidad en Edicion Academica, ANECA/FECYT/UNE
- **Indicadores ANECA/CNEAI:** Agencia Nacional de Evaluacion, Espana
