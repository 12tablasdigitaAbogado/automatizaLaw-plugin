---
name: nomina-documental
description: >-
  Arma la nómina/índice de documentación para presentar la demanda laboral (parte
  trabajadora): cruza la prueba documental que la demanda dice ofrecer contra lo que
  realmente existe en la carpeta del cliente, ordena la nómina según el fuero, y
  marca qué falta antes de presentar. Usá esta skill cuando el usuario diga cosas como
  "armá la nómina de documentación", "preparame los adjuntos de la demanda", "¿qué
  documentación falta para presentar?", "armá el paquete de la demanda", "chequeá que
  tengamos todo para presentar", "índice de prueba documental". No redacta la demanda
  ni arma el PDF final — es el paso de control antes de presentar.
---

# Nómina documental (parte trabajadora)

Armá la nómina/índice de la documentación que se va a presentar junto con la demanda, cruzando lo que la demanda dice ofrecer contra lo que realmente está disponible en la carpeta del cliente. Es un **control previo a la presentación**, no un trámite ante el juzgado.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Preciso y desconfiado por diseño: no dar nada por presentado sin verificarlo.

**Salida única (determinística):** la nómina de documentación (con lo disponible y lo faltante), mostrada en el chat y guardada como archivo nuevo en la carpeta del cliente. La skill NO arma el PDF final, NO presenta, NO notifica.

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio (conectada a Cowork, sincronizada con Drive por Google Drive para Escritorio). Encontralo (Glob/Grep por nombre) y tomá su carpeta contenedora como la raíz; buscá `modelos/`, `datos/` y `clientes/` dentro de esa raíz. Tratá todo como sistema de archivos local (Read/Write); no uses el conector/API de Google Drive.

Leé `perfil_estudio.md` y tomá: **fuero/jurisdicción** del caso (define el orden y las convenciones esperadas de la nómina), y si el organismo usa **presentación electrónica** con alguna convención de nombrado de archivos. Si no lo encontrás, seguí igual con el orden estándar del Paso 3 y avisá que trabajaste sin perfil.

## Paso 1 — Identificar el caso y reunir lo que ya existe

Identificá de qué cliente/expediente es (si no surge, preguntá) y buscá en `clientes/<cliente>/` todo lo relacionado:

- La **demanda** redactada (de la skill de Demanda Laboral) — de ahí sale la lista de prueba documental ofrecida (su Paso 8).
- La **liquidación** (de la skill de Liquidación de Rubros).
- Los **telegramas/CD** enviados y las respuestas del empleador (de la skill de Telegrama/Carta Documento).
- Cualquier otra **documentación aportada por el cliente**: recibos de sueldo, DNI, certificados, constancias, contrato, etc.

Si no encontrás la demanda en la carpeta, pedí que la peguen o generen primero — sin ella no hay contra qué cruzar la documental.

## Paso 2 — Cruzar la prueba documental ofrecida contra lo disponible

Tomá la lista de prueba documental del Paso 8 de la demanda (documental, y cualquier otra que mencione explícitamente: recibos, telegramas y respuestas, DNI, constancias, certificados, contrato, CCT aplicable, etc.). Para cada ítem:

- **Buscalo en la carpeta del cliente.** Si existe un archivo que corresponde, marcalo como **disponible** y anotá el nombre del archivo.
- **Si no lo encontrás, marcalo como FALTANTE.** No asumas que "seguramente está" ni lo complete inventando una referencia — la ausencia se reporta, no se disimula.
- Si un ítem de la demanda es ambiguo (p. ej. "documentación de la relación laboral" sin especificar cuál), pedí precisión en vez de adivinar qué archivo cuenta.

## Paso 3 — Ordenar la nómina según el fuero

Armá la nómina en el orden que indique el perfil para ese fuero/organismo — el perfil siempre pisa lo que sigue. Si no especifica un orden, usá esta guía según la jurisdicción (investigada, no inventada; actualizarla si cambia la normativa):

**Nación / CABA (Justicia Nacional del Trabajo):** tiene instancia previa obligatoria de conciliación ante el SECLO. Orden: (1) constancia de cierre del SECLO, (2) formulario de inicio + poder/acta poder certificada, (3) escrito de demanda, (4) DNI del trabajador, (5) documental digitalizada en el orden en que se cita en el cuerpo de la demanda (recibos, telegramas y respuestas, certificados, otra documental), (6) liquidación si el organismo la exige como pieza separada.

**Provincia de Buenos Aires (SCBA — MEV/Augusta):** **no tiene instancia previa de conciliación** en lo laboral (a diferencia de Nación — tenelo en cuenta también para lo que arme `jurisdiccion-competencia`). Orden: (1) escrito de demanda, (2) DNI del trabajador, (3) carta poder/poder, (4) toda la prueba documental completa, (5) constancia de mediación previa si la hubo, (6) solicitud de radicación en el juzgado sorteado.

**Córdoba (Fuero del Trabajo — sistema SAC):** la presentación electrónica estructura por partes (humana/jurídica) con un check de "usar poder", no por una lista lineal de adjuntos. No hay una convención pública de orden documental tan clara como en los otros dos fueros — para Córdoba, apoyate más en lo que diga el perfil del estudio que en este default, y si el perfil no lo tiene, avisá que el orden es orientativo y no una norma verificada para ese fuero puntual.

**Otras jurisdicciones no investigadas todavía:** usá este orden genérico y avisá que es un default sin verificar para ese fuero: (1) poder, (2) DNI, (3) recibos/documentación registral, (4) telegramas y respuestas, (5) certificados art. 80, (6) otra documental, (7) liquidación.

## Paso 4 — Entregar

Mostrá la nómina completa en una tabla: **# | Documento | Disponible/Faltante | Archivo (si existe)**. Arriba de todo, un resumen de cuántos ítems faltan y cuáles son — eso es lo que el abogado necesita ver primero, no el listado completo.

Guardá la nómina como archivo nuevo en la carpeta del cliente: `nomina-documental-<cliente>-<AAAA-MM-DD>.docx`. No pises nada ni mezcles clientes.

## Guardrails duros (no negociar)

- **Nunca marcar un ítem como disponible sin haber encontrado el archivo correspondiente.** Ante la duda, es faltante.
- **Nunca declarar la nómina "completa" si falta el poder, el DNI, o cualquier documental que la demanda mencione explícitamente como ofrecida.** Esos son los que más comprometen la presentación.
- Si el fuero exige convención de nombrado o formato para presentación electrónica y algún archivo no la cumple, señalalo — no renombres ni conviertas archivos por tu cuenta.
- Todo es **checklist de control para revisión del abogado**, no una certificación de que el legajo está listo para presentar.

## Conexión con otras skills

Se nutre de **Demanda Laboral** (la prueba documental ofrecida), **Liquidación de Rubros** (el archivo de la liquidación) y **Telegrama/Carta Documento** (el intercambio telegráfico). Si hay ítems faltantes, el paso siguiente es de gestión manual del estudio (pedirlos al cliente), no de otra skill.

## Nota de verificación

Al terminar, indicá: cuántos ítems cruzaste, cuántos están disponibles y cuántos faltan (con el detalle de cada faltante), si pudiste leer el perfil, y qué orden de fuero aplicaste. El orden de Nación/CABA y Provincia de Buenos Aires está investigado sobre fuentes oficiales (Acordadas CSJN, SCBA); el de Córdoba y el de cualquier otra jurisdicción no listada es orientativo, no verificado fuero por fuero — decilo explícitamente cuando se use. Es un checklist de control previo a la presentación — la decisión de presentar igual, con lo que falta pendiente, es del abogado.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. `perfil_estudio.md` está en `.md` y se lee con `Read` normal. **Los modelos del estudio (todo lo que cuelga de `modelos/`) están en Word `.docx`: extraé su texto con la skill `docx`, nunca con `Read` directo (un `.docx` abierto con `Read` devuelve el binario comprimido, no el texto).** La única salida/insumo que no es `.docx` es la calculadora de liquidación, que es Excel `.xlsx`. Si algún modelo puntual estuviera en `.md`, ese sí se lee con `Read`.
