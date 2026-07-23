---
name: alegato
description: Prepara el alegato (o alegato de bien probado) en un juicio laboral (parte trabajadora): sintetiza toda la prueba producida y la orienta al pedido concreto de sentencia. Usá esta skill SIEMPRE que el usuario diga cosas como "preparame el alegato", "armá el alegato", "alegato de bien probado", "qué alego en la vista de causa", "cerrame el caso con la prueba producida". Devuelve un guión para alegato verbal o un escrito, según la jurisdicción del perfil. Es material para la audiencia / borrador para el abogado.
---

# Alegato (parte trabajadora)

Producí el alegato: tomá toda la prueba producida en el expediente y construí el cierre orientado a que el tribunal haga lugar a la demanda. Según la jurisdicción, sale como **guión para alegato verbal** (vista de causa oral) o como **escrito**.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Argumentación persuasiva, técnica y ordenada; sin sobrecarga doctrinaria. No agregues advertencias del tipo "esto no es asesoramiento legal".

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio (conectada a Cowork y sincronizada con Drive por Google Drive para Escritorio). Encontralo (Glob/Grep por nombre) y tomá su **carpeta contenedora como la raíz del estudio**. Todas las demás carpetas — `modelos/`, `datos/` y `clientes/` — están **dentro de esa raíz**: buscalas ahí, nunca como nombres sueltos. Tratá todo como sistema de archivos local: leé con Read y guardá con Write; no uses el conector/API de Google Drive.

Antes de nada, buscá (Glob/Grep) y leé con Read `perfil_estudio.md` en la carpeta del estudio. Tomá: jurisdicción y fuero (define si el alegato es verbal o escrito), criterios, doctrina/fallos de cabecera, tasa de interés y estilo. Si no lo encontrás, seguí igual y avisá que trabajaste sin perfil.

## Paso 1 — Leer el modelo (carpeta local, solo lectura)

Buscá en `modelos/escritos/` el modelo de alegato del estudio (por palabra clave) y leelo: tomá su estructura, estilo argumentativo y forma de organizar el mérito de la prueba. Si no hay un modelo para esto, usá la estructura estándar del Paso 4 y avisá. No modifiques el modelo.

## Paso 2 — Reunir la prueba producida

Pedí o reuní lo que esté disponible: la **testimonial** (qué declaró cada testigo), la **absolución de posiciones / confesional** (si existe en esa jurisdicción), la **pericial** (y si hubo impugnación), la **documental** y la **informativa** (respuestas a oficios). Sumá la **demanda** y la **contestación** para tener los hechos controvertidos. Si ya se corrieron las skills de *Análisis de Contestación* y *Preparación Testimonial*, aprovechá sus salidas. Pedí lo que falte.

## Paso 3 — Mérito de la prueba, hecho por hecho

Para cada hecho controvertido relevante (relación y su real extensión, jornada y horas extras, categoría, remuneración real, causal de la injuria o improcedencia del despido, **conocimiento del empleador sobre el embarazo/matrimonio** o **estado de salud/licencia al momento del despido** —si el caso es de esa clase—, etc.), mostrá **con qué prueba quedó acreditado** (qué testigo, qué documento, qué tramo de la pericia). Conectá cada hecho probado con el **rubro reclamado** que sostiene. Señalá por qué la prueba de la contraria no alcanza.

## Paso 4 — Redactar el alegato

Seguí la estructura del modelo del estudio si lo encontraste en el Paso 1; si no había, armá: (a) introducción y objeto; (b) mérito de la prueba hecho por hecho (lo del Paso 3); (c) refutación de las defensas del demandado; (d) encuadre jurídico con la doctrina/fallos y la tasa del perfil (sin sobrecargar) — **nunca cites un fallo, plenario o doctrina que no hayas podido verificar en el momento**, sin excepción, sin importar cuán segura te "suene" la referencia; ante la duda, se omite, y si hace falta investigación jurídica de fondo, complementá con **Investigación Jurídica**; (e) conclusión y petitorio (que se haga lugar a la demanda, con el alcance pretendido).

Entregá guión para alegato verbal o escrito según el perfil. Mostralo y **guardalo como archivo nuevo en la carpeta del cliente, bajo `clientes/<cliente>/`**. Esa es su salida: el alegato en el chat más el archivo en la carpeta del cliente. No ejecuta otras acciones.

## Conexión con otras skills

Se nutre de **Análisis de Contestación** y **Preparación Testimonial**, y suele acompañarse de la **liquidación actualizada** a la fecha de la audiencia. Ofrecé encadenar si el usuario sigue.

## Cómo ubicar la carpeta del cliente (antes de guardar)

1. Identificá de qué **cliente / expediente** es la salida. Si no surge claro del contexto, preguntalo (nombre del cliente o carátula).
2. Buscá (Glob) la carpeta de ese cliente dentro de `clientes/`.
3. Si **existe**, guardá ahí. Si **no existe**, creala dentro de `clientes/` y después guardá.
4. Nombrá el archivo de forma descriptiva: `<tipo>-<cliente>-<AAAA-MM-DD>.docx`. Nunca mezcles archivos de distintos clientes ni pises uno existente.

## Nota de verificación

Al terminar, indicá qué prueba pudiste integrar, si leíste el perfil, y si el formato es verbal o escrito. Es material para la audiencia / **borrador para el criterio del abogado**.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. Los archivos del cerebro del estudio (`perfil_estudio.md` y todo lo que cuelga de `modelos/`) siguen en `.md` y se leen con `Read` normal.
