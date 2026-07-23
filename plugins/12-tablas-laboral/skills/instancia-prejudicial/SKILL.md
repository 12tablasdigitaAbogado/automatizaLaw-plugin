---
name: instancia-prejudicial
description: >-
  Determina si el reclamo laboral (despido, salarios, registración y afines — no
  cubre accidentes/enfermedades laborales bajo Ley 24.557) necesita agotar una
  instancia administrativa previa obligatoria antes de poder demandar, según la
  jurisdicción del caso. La fuente principal es el perfil del estudio (el dato se
  carga una vez en el alta); si el perfil no lo tiene, usa como referencia verificada
  Nación/CABA (SECLO obligatorio), Provincia de Buenos Aires y Córdoba (sin instancia
  previa administrativa — la conciliación es intraprocesal), y para cualquier otra
  jurisdicción avisa que no está verificado en vez de asumir. Usá esta skill cuando
  el usuario diga cosas como "¿hay que pasar por conciliación antes?", "¿necesito el
  SECLO?", "instancia previa", "¿puedo demandar directo o hay un paso antes?", o
  cuando definas la jurisdicción de un caso y falte confirmar este punto antes de la
  demanda.
---

# Instancia prejudicial (parte trabajadora — reclamos comunes)

Determinás si el reclamo necesita agotar una instancia administrativa previa antes de poder demandar, y guiás el trámite si corresponde. **Alcance: reclamos laborales comunes (despido, salarios, registración, certificados, hostigamiento, etc.).** No cubre accidentes de trabajo ni enfermedades profesionales (Ley 24.557) — eso queda fuera del alcance de este estudio y de esta skill.

**Salida:** un resumen de si corresponde instancia previa, cuál, ante qué organismo, y qué constancia guardar para la demanda y la nómina documental. Se muestra en el chat y se guarda en la carpeta del cliente si el caso ya tiene una.

## Paso 0 — Buscar primero la respuesta en el perfil del estudio

Leé `perfil_estudio.md` (Glob/Grep por nombre en la carpeta del estudio). Buscá específicamente si tiene cargado un dato del tipo "instancia previa obligatoria: sí/no, ante qué organismo" para la jurisdicción de ese estudio — este es el dato que se completa una vez en el alta y vale para todos los casos de ese estudio.

- **Si el perfil ya lo tiene:** usalo directamente, no hace falta nada más. Pasá al Paso 2.
- **Si el perfil no lo tiene:** pasá al Paso 1.

## Paso 1 — Sin dato en el perfil: usar la referencia verificada, o avisar que falta

Con la jurisdicción del caso (de `jurisdiccion-competencia` o de la ficha de primera consulta, si ya existen; **si ninguna de las dos está, preguntale la jurisdicción directamente al usuario** — no sigas sin ese dato):

- **Nación / CABA (Justicia Nacional del Trabajo):** instancia previa **obligatoria** ante el **SECLO** (Ley 24.635), salvo excepciones legales (amparos y cautelares, diligencias preliminares y prueba anticipada, reclamos de procedimientos de crisis de las leyes 24.013/14.786, demandas contra empleador concursado o quebrado, demandas contra el Estado nacional/provincial/municipal, acciones de menores que requieran intervención del Ministerio Público). Gratuita para el trabajador. Sin el certificado de cierre, el juzgado puede no dar curso a la demanda (art. 65 Ley 24.635).
- **Provincia de Buenos Aires (SCBA):** **no** tiene instancia previa administrativa obligatoria. La conciliación ocurre dentro del proceso judicial ya iniciado, en audiencia ante el juzgado.
- **Córdoba (Fuero del Trabajo, Ley 7987/10.596):** tampoco tiene instancia previa administrativa. La conciliación es una audiencia dentro del proceso (arts. 49/50/83 quinquies), después de contestada la demanda.
- **Cualquier otra jurisdicción:** **no está verificado.** Decilo explícitamente, no asumas ni que sí ni que no hay instancia previa. Sugerí confirmarlo con una fuente oficial de esa provincia y **cargar el dato en el perfil del estudio** para que la próxima vez ya esté disponible sin tener que volver a investigarlo.

## Paso 2 — Entregar

Un resumen con: (1) jurisdicción identificada, (2) si corresponde instancia previa y cuál (o "sin instancia previa — conciliación intraprocesal", o "no verificado para esta jurisdicción"), (3) organismo y trámite si corresponde, (4) qué constancia final hay que guardar para la demanda y la nómina documental, (5) si corresponde, recordá activar en `plazos-procesales` la suspensión de la prescripción mientras dura el trámite. Si el dato vino del Paso 1 (no del perfil), sugerí agregarlo al perfil del estudio para la próxima consulta.

## Guardrails duros (no negociar)

- **La fuente de verdad es el perfil del estudio.** Los tres casos verificados (Nación/CABA, PBA, Córdoba) son una referencia de respaldo para cuando el perfil todavía no tiene el dato — no reemplazan lo que el perfil diga si lo tiene cargado.
- **Ante una jurisdicción no verificada y sin dato en el perfil, nunca asumas "no hay instancia previa" ni "sí la hay" por default.** Decilo como pendiente de confirmar.
- **No inventes plazos, formularios o requisitos operativos puntuales que no verificaste** (duración real de un trámite de SECLO, formulario vigente, sitio de gestión). Remití a la fuente oficial en vez de aproximar.
- Esta skill no contempla accidentes de trabajo ni enfermedades profesionales (Ley 24.557) — si el usuario consulta por uno, avisá que ese tipo de caso está fuera del alcance de este estudio/paquete, no lo resuelvas.

## Conexión con otras skills

Se nutre del **perfil del estudio** (fuente primaria) y, en su ausencia, de **Jurisdicción y Competencia** (fuero) y la **ficha de primera consulta**. Si corresponde instancia previa, avisá para activar el seguimiento del plazo en **Plazos Procesales** y para que **Nómina Documental** incluya el certificado de cierre como primer documento. Alimenta directamente a **Demanda Laboral**.

## Nota de verificación

Al terminar, indicá: si la respuesta vino del perfil del estudio o de la referencia verificada (Nación/CABA, PBA, Córdoba), o si quedó marcada como no verificada. Si fue esto último, recordá sugerir que se cargue en el perfil una vez confirmada. Es un chequeo de camino procesal, no un dictamen legal — la decisión de cómo tramitarlo es del abogado.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. `perfil_estudio.md` está en `.md` y se lee con `Read` normal. **Los modelos del estudio (todo lo que cuelga de `modelos/`) están en Word `.docx`: extraé su texto con la skill `docx`, nunca con `Read` directo (un `.docx` abierto con `Read` devuelve el binario comprimido, no el texto).** La única salida/insumo que no es `.docx` es la calculadora de liquidación, que es Excel `.xlsx`. Si algún modelo puntual estuviera en `.md`, ese sí se lee con `Read`.
