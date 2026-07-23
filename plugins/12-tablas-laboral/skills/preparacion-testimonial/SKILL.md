---
name: preparacion-testimonial
description: Prepara la prueba testimonial en un juicio laboral (parte trabajadora): a partir de las debilidades del caso y de las defensas del empleador, arma un punteo por testigo con los hechos que cada uno debería reforzar en la audiencia. Usá esta skill SIEMPRE que el usuario diga cosas como "preparar a los testigos", "qué tiene que reforzar cada testigo", "puntos para la testimonial", "preparación testimonial", "qué le pregunto a los testigos", "ayudame con los testigos antes de la audiencia". Devuelve un punteo estratégico interno para el abogado, no un escrito judicial.
---

# Preparación testimonial (parte trabajadora)

Producí un punteo de preparación de testigos: para cada testigo, qué hechos puede acreditar y qué debería reforzar en la audiencia según las debilidades del caso y las defensas opuestas por el empleador. Es material interno para que el abogado prepare a sus testigos, NO un escrito para presentar.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Criterio estratégico, preciso, directo. No agregues advertencias del tipo "esto no es asesoramiento legal".

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio (conectada a Cowork y sincronizada con Drive por Google Drive para Escritorio). Encontralo (Glob/Grep por nombre) y tomá su **carpeta contenedora como la raíz del estudio**. Todas las demás carpetas — `modelos/`, `datos/` y `clientes/` — están **dentro de esa raíz**: buscalas ahí, nunca como nombres sueltos. Tratá todo como sistema de archivos local: leé con Read y guardá con Write; no uses el conector/API de Google Drive.

Antes de nada, buscá (Glob/Grep) y leé con Read `perfil_estudio.md` en la carpeta del estudio. Tomá: jurisdicción y fuero (define cómo se rinde la testimonial y si los testigos se citan de oficio o por cédula), criterios y estilo del estudio. Si no lo encontrás, seguí igual y avisá que trabajaste sin perfil.

## Paso 1 — Reunir los insumos

- **Hechos controvertidos y debilidades.** Si ya se corrió la skill de *Análisis de Contestación*, tomá su salida (defensas opuestas, hechos negados, puntos débiles). Si no está, pedí o reuní la demanda + la contestación + el intercambio telegráfico para identificarlos vos.
- **Los testigos.** Pedí al usuario, para cada testigo: nombre, vínculo con el trabajador y la empresa, período en que trabajó o presenció los hechos, y qué le consta de primera mano. Sin esto, no asignes hechos a testigos: pedilo.

## Paso 2 — Determinar qué hay que probar

Listá los **hechos controvertidos favorables al trabajador** que dependen de la testimonial (los que el demandado negó: existencia o real extensión de la relación, jornada y horas extras, categoría y tareas, fecha de ingreso, pagos en negro, hostigamiento, hechos de la injuria, **conocimiento del empleador sobre el embarazo/matrimonio y cómo se enteró** —si el caso es de esa clase—, **estado de salud o licencia médica del trabajador al momento del despido** —si el caso es de enfermedad inculpable/reserva de puesto—, etc.) y los **puntos débiles propios** a apuntalar.

## Paso 3 — Punteo por testigo

Para cada testigo, devolvé:

- **Qué puede acreditar** (solo lo que le consta de primera mano; no forzar testimonio sobre lo que no presenció).
- **Qué debe enfatizar** para los hechos controvertidos donde ese testigo es útil.
- **Consistencia**: que su relato no choque con los telegramas, la demanda ni con otros testigos.
- **Riesgos / repregunta**: dónde puede atacar la contraria y cómo evitar contradicciones.
- (Opcional) **preguntas orientativas** del lado actor, si el usuario las quiere.

Tené presente que entre el despido y la audiencia pueden pasar años: sumá un recordatorio de repasar los hechos con el testigo antes de declarar.

## Paso 4 — Entregar

Mostrá el punteo organizado por testigo, con un resumen inicial de los hechos a probar, y **guardalo como archivo nuevo en la carpeta del cliente, bajo `clientes/<cliente>/`**. Esa es su salida: el punteo en el chat más el archivo en la carpeta del cliente. No ejecuta otras acciones. Es material interno: el testigo declara con la verdad de lo que le consta; esto orienta, no arma un libreto falso.

## Conexión con otras skills

Se nutre de **Análisis de Contestación** (skill previa) y alimenta la **Vista de causa / Alegato**. Ofrecé encadenar si el usuario sigue.

## Cómo ubicar la carpeta del cliente (antes de guardar)

1. Identificá de qué **cliente / expediente** es la salida. Si no surge claro del contexto, preguntalo (nombre del cliente o carátula).
2. Buscá (Glob) la carpeta de ese cliente dentro de `clientes/`.
3. Si **existe**, guardá ahí. Si **no existe**, creala dentro de `clientes/` y después guardá.
4. Nombrá el archivo de forma descriptiva: `<tipo>-<cliente>-<AAAA-MM-DD>.docx`. Nunca mezcles archivos de distintos clientes ni pises uno existente.

## Nota de verificación

Al terminar, indicá qué insumos usaste (análisis previo o documentos sueltos), si leíste el perfil, y qué te faltó. Material interno para el criterio del abogado.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. Los archivos del cerebro del estudio (`perfil_estudio.md` y todo lo que cuelga de `modelos/`) siguen en `.md` y se leen con `Read` normal.
