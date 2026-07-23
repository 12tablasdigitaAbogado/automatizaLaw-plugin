---
name: ofrecimiento-prueba
description: >-
  Redacta el escrito de ofrecimiento de prueba de la parte trabajadora, para las
  jurisdicciones donde es un acto procesal separado de la demanda (posterior a la
  audiencia de conciliación y a la contestación — ej. Córdoba, procedimiento
  ordinario). No es un escrito de mero trámite: cruza los hechos que quedaron
  controvertidos tras la contestación para decidir qué prueba conviene ofrecer en
  esta etapa (documental adicional, testimonial con sus puntos, pericial con los
  puntos de pericia, confesional, informativa) y con qué fundamento. Usá esta skill
  cuando el usuario diga cosas como "ofrecé la prueba", "armá el ofrecimiento de
  prueba", "qué prueba ofrezco después de la contestación", "toca ofrecer prueba en
  este caso". Antes de usarla, confirmá que la jurisdicción del caso trata esto como
  acto separado (perfil del estudio, o consultá con el abogado si no está cargado) —
  en jurisdicciones donde la prueba va incluida en la demanda, no corresponde este
  escrito, ya se hizo en Demanda Laboral.
---

# Ofrecimiento de prueba (parte trabajadora)

Redactás el ofrecimiento de prueba como acto procesal separado, en las jurisdicciones donde corresponde. No es completar un modelo en blanco: el criterio central de esta skill es decidir **qué prueba conviene ofrecer en esta etapa**, cruzando lo que quedó controvertido después de la contestación — por eso vive aparte de escritos-tramite, que solo cubre escritos sin razonamiento nuevo.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Criterio estratégico sobre la prueba, terminología procesal precisa.

**Salida:** el escrito de ofrecimiento de prueba, mostrado en el chat y guardado como archivo nuevo en la carpeta del cliente.

## Paso 0 — Confirmar que corresponde este escrito (no asumir)

Leé `perfil_estudio.md` (Glob/Grep por nombre, carpeta contenedora como raíz del estudio). Buscá el dato de si, en la jurisdicción del caso, el ofrecimiento de prueba es un acto separado de la demanda o va incluido en ella.

- **Si el perfil ya lo tiene:** usalo directamente.
- **Si el perfil no lo tiene:** usá como referencia verificada — Nación/CABA y Provincia de Buenos Aires: va incluido en la demanda, **esta skill no corresponde**, avisá y derivá (ya se hizo en demanda-laboral). Córdoba: depende del procedimiento — en el PDA va incluido en la demanda (no corresponde esta skill); en el procedimiento ordinario es un acto separado (Ley 7987, art. 52) y **sí corresponde**. Para **cualquier otra jurisdicción no verificada**, no asumas ninguna de las dos opciones: avisá que hay que confirmarlo antes de seguir, y sugerí cargar la respuesta en el perfil del estudio para la próxima vez.

Si corresponde el escrito, seguí al Paso 1.

## Paso 1 — Reunir el material del caso

Buscá en `clientes/<cliente>/` (o pedí si no está): la **demanda** (qué se dijo, qué prueba documental ya se adjuntó), la **contestación** del empleador, y si ya se corrió, la salida de **Análisis de Contestación** (hechos negados/reconocidos, puntos débiles, contradicciones). Si no se corrió esa skill, podés ofrecer encadenar antes de seguir, o reunir vos directamente demanda + contestación para identificar los hechos controvertidos. Pedí lo que falte.

## Paso 2 — Decidir qué prueba ofrecer

Para cada hecho que quedó controvertido (no admitido por el demandado), determiná qué prueba corresponde y por qué:

- **Documental**: si hay documentos que no se ofrecieron en la demanda (porque no se tenían entonces, o porque surgieron de la propia contestación) y ahora corresponde agregar.
- **Testimonial**: qué testigos proponer y sobre qué hechos controvertidos puede declarar cada uno (no ofrezcas un testigo sin conexión clara a un hecho controvertido).
- **Pericial**: si corresponde (contable para diferencias salariales, u otra según el caso), con los puntos de pericia concretos.
- **Confesional / absolución de posiciones**: si la jurisdicción la prevé.
- **Informativa**: qué oficios conviene librar y a qué organismos.

No ofrezcas prueba que no exista o que no se pueda producir realmente — si falta un dato para fundar un ofrecimiento (por ejemplo, no tenés el nombre completo de un testigo), pedilo antes de inventarlo.

## Paso 3 — Redactar el escrito

Buscá el modelo del estudio en `modelos/escritos/` (si existe uno para ofrecimiento de prueba); si no hay, usá una estructura estándar: objeto, prueba ofrecida organizada por tipo (documental, testimonial con los testigos y su domicilio si corresponde, pericial con los puntos, confesional, informativa), y petitorio. Mostralo y guardalo como archivo nuevo en `clientes/<cliente>/`.

## Guardrails duros (no negociar)

- **Nunca asumas si corresponde este escrito sin chequear el perfil o confirmarlo con el abogado** — la mitad de las jurisdicciones no lo necesitan porque la prueba ya se ofreció en la demanda.
- **No ofrezcas prueba inexistente o sin fundamento en un hecho controvertido real.**
- **No repitas sin criterio toda la prueba de la demanda** — el valor de esta skill es decidir qué hace falta ahora, a la luz de la contestación, no copiar y pegar el ofrecimiento original.

## Conexión con otras skills

Se nutre de la **Demanda** y de **Análisis de Contestación** (hechos controvertidos). Los testigos que se terminen ofreciendo acá son los que después prepara **Preparación Testimonial** para la audiencia — avisá esa conexión si el usuario sigue.

## Nota de verificación

Al terminar, indicá: si el perfil ya tenía el dato de la jurisdicción o si usaste la referencia verificada (o si quedó sin confirmar), qué prueba ofreciste y con qué hecho controvertido la conectaste, y qué te faltó. Borrador para revisión y firma del abogado.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. Los archivos del cerebro del estudio (`perfil_estudio.md` y todo lo que cuelga de `modelos/`) siguen en `.md` y se leen con `Read` normal.
