---
name: telegrama-carta-documento
description: Redacta la intimación obrera (telegrama ley 23.789 o carta documento) de la parte trabajadora, según el supuesto: intimación a registrar o aclarar la situación, sub-registración, hostigamiento, diferencias salariales / horas extras, entrega de certificados (art. 80 LCT), despido indirecto / autodespido, enfermedad inculpable / reserva de puesto, notificación de embarazo o matrimonio, o rechazo de la misiva del empleador. Usá esta skill cuando el usuario diga cosas como "armá un telegrama", "carta documento", "intimá a registrar", "intimá los haberes / diferencias", "intimá los certificados art. 80", "telegrama de despido indirecto / autodespido", "aviso de enfermedad", "notificá el embarazo", "TCL", "CD", "rechazá la carta del empleador". Lee el perfil y el modelo de telegrama desde la carpeta del estudio y guarda el borrador en la carpeta del cliente. Borrador para revisión y firma del abogado.
---

# Telegrama / carta documento (parte trabajadora)

Redactá la intimación obrera lista para revisar, según el supuesto, tomando como base el modelo del estudio. Los supuestos, con su articulado y apercibimiento, están en `references/supuestos-telegrama.md`.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Estructura formal de carta documento: remitente, destinatario, relato sucinto, intimación concreta, plazo expreso y apercibimiento. Tono intimatorio y en presente ("Intimo a Ud. …"), texto continuo apto para el formulario del Correo (ley 23.789). No agregues advertencias del tipo "esto no es asesoramiento legal".

**Salida única (determinística):** el texto de la carta documento / telegrama, mostrado en el chat y guardado como archivo nuevo en la carpeta del cliente. La skill NO envía, NO notifica y NO ejecuta ninguna otra acción.

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio (conectada a Cowork, sincronizada con Drive por Google Drive para Escritorio). Encontralo (Glob/Grep por nombre) y tomá su carpeta contenedora como la raíz; buscá `modelos/`, `datos/` y `clientes/` dentro de esa raíz. Tratá todo como sistema de archivos local (Read/Write); no uses el conector/API de Google Drive.

Leé `perfil_estudio.md` y tomá: jurisdicción, **plazos** que usa el estudio (p. ej. 48 hs; 30 días para certificados art. 80), si suma **datos de contacto al pie** (para habilitar la negociación), estilo, pie de firma, y el criterio **24.013 vs reparación integral**. Si no lo encontrás, detené y pedí completar el alta.

## Paso 1 — Detectar el supuesto

Identificá cuál corresponde (ver `references/supuestos-telegrama.md`): registración / aclaración, sub-registración, hostigamiento, diferencias salariales u horas extras, certificados (art. 80 LCT), despido indirecto / autodespido, enfermedad inculpable / reserva de puesto, notificación de embarazo o matrimonio, o rechazo de misiva. Puede haber **más de uno** en una misma misiva. Al generar el **despido indirecto**, ofrecé sumar en el mismo lote la intimación de **art. 80** y la de **pago**.

## Paso 2 — Leer el modelo (carpeta local, solo lectura)

Buscá en `modelos/telegramas/` el modelo del supuesto detectado (por palabra clave) y leelo: tomá su estructura, sus fórmulas de estilo, el articulado citado y las cláusulas de apercibimiento. Si no hay un modelo para ese supuesto, usá la estructura estándar de `references/supuestos-telegrama.md` y avisá. No modifiques el modelo.

## Paso 3 — Pedir los datos del caso

Pedí en una sola tanda: **trabajador/a (remitente)** nombre, DNI y domicilio; **empleador/a (destinatario)** denominación y domicilio donde se notifica; datos de la relación (ingreso, categoría/CCT, jornada, remuneración, situación registral); **hechos** que fundan la intimación; **objeto** concreto de cada intimación; **plazo** (si no se indica, usá el del perfil); y **apercibimiento**. Si falta un dato esencial (destinatario, objeto, plazo o apercibimiento), preguntalo antes de redactar.

## Paso 4 — Redactar

Seguí la forma del modelo: encabezado con remitente y destinatario; cuerpo intimatorio con relato sucinto; cada intimación con su **plazo expreso** y su **apercibimiento**, citando el articulado pertinente (art. 11 ley 24.013, arts. 242 y 246 LCT, art. 80 LCT y dec. 146/01, etc.). Texto continuo, sin formato decorativo. Cerrá con el pie de firma del estudio (y los datos de contacto si el perfil lo indica).

## Paso 5 — Guardar en la carpeta del cliente

Entregá el texto en el chat y guardalo como archivo nuevo en la carpeta del cliente.

1. Identificá de qué cliente/expediente es; si no surge, preguntá.
2. Buscá por nombre la carpeta del cliente dentro de `clientes/`.
3. Si existe, guardá ahí; si no, creala (o pedí que la creen) y guardá.
4. Nombrá el archivo `telegrama-<supuesto>-<cliente>-<AAAA-MM-DD>.docx`. No pises nada ni mezcles clientes.

## Nota de verificación

Al terminar, indicá: el/los supuesto(s), qué modelo del estudio usaste (o que no había), qué datos te faltaron, el plazo y el apercibimiento, y dónde guardaste el borrador. Es **borrador para revisión y firma del abogado**.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. Los archivos del cerebro del estudio (`perfil_estudio.md` y todo lo que cuelga de `modelos/`) siguen en `.md` y se leen con `Read` normal.
