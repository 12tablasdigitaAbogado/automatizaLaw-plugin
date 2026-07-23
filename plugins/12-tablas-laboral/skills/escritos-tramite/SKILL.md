---
name: escritos-tramite
description: Redacta los escritos de trámite del proceso laboral (parte trabajadora) que no requieren razonamiento nuevo y se completan desde un modelo del estudio: poder, segundo traslado / réplica a la contestación, pedido de apertura a prueba, cédulas (de notificación y de prueba), oficios y su acreditación, acuerdos conciliatorios (extrajudicial, homologación directa, durante el trámite), escrito de inicio de ejecución de sentencia, recursos de revocatoria/aclaratoria (contra una providencia, NO una apelación de sentencia) y rebeldía. Usá esta skill cuando el usuario pida cualquiera de esos escritos: "armá el poder", "el segundo traslado", "pedí apertura a prueba", "la cédula de…", "el oficio a…", "acreditá el oficio", "el acuerdo conciliatorio", "iniciá la ejecución", "interponé revocatoria/aclaratoria", "acusá la rebeldía". NO cubre telegrama ni demanda (otras skills), NI apelación de sentencia (expresión de agravios — eso es la skill Recurso de Apelación), NI el ofrecimiento de prueba como acto separado (eso es la skill Ofrecimiento de Prueba, requiere criterio sobre qué prueba conviene, no es de mero trámite), ni el pacto de cuota litis (lo genera Contrato de Honorarios). Lee el perfil y el modelo correspondiente desde la carpeta del estudio y guarda el borrador en la carpeta del cliente.
---

# Escritos de trámite (parte trabajadora)

Completá un escrito de trámite desde el modelo del estudio. Son escritos estandarizados que no requieren razonamiento jurídico nuevo: la sustancia la aporta el modelo + los datos del caso. El catálogo de tipos, con qué modelo usa y qué datos pide cada uno, está en `references/catalogo-escritos.md`.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Terminología procesal precisa, formato formal. No agregues advertencias del tipo "esto no es asesoramiento legal".

**Salida única (determinística):** el escrito redactado, mostrado en el chat y guardado como archivo nuevo en la carpeta del cliente. La skill NO notifica, NO presenta y NO ejecuta ninguna otra acción.

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio (conectada a Cowork y sincronizada con Drive por Google Drive para Escritorio). Encontralo (Glob/Grep por nombre) y tomá su **carpeta contenedora como la raíz del estudio**. Todas las demás carpetas — `modelos/`, `datos/` y `clientes/` — están **dentro de esa raíz**: buscalas ahí, nunca como nombres sueltos. Tratá todo como sistema de archivos local: leé con Read y guardá con Write; no uses el conector/API de Google Drive.

Buscá (Glob/Grep) y leé con Read `perfil_estudio.md`: jurisdicción y fuero, formato local (las cédulas y oficios cambian de formato según el sistema judicial), estilo y pie de firma. Si no lo encontrás, detené y pedí completar el alta.

## Paso 1 — Identificar el escrito

Determiná cuál de los escritos de trámite del catálogo (`references/catalogo-escritos.md`) pide el usuario. Si no queda claro, preguntá cuál. Si lo que piden es un telegrama, una demanda o un pacto de cuota litis, derivá a la skill que corresponde (no es esta).

## Paso 2 — Leer el modelo (carpeta local, solo lectura)

Listá (Glob) la carpeta `modelos/escritos/`, elegí el modelo `.docx` de ese escrito y extraé su texto con la skill `docx` (los modelos son Word `.docx`, no uses `Read` directo). Tomá su estructura, fórmulas, articulado y formato. No modifiques el modelo.

**Si no hay un modelo, pero el tipo de escrito SÍ está en el catálogo** (`references/catalogo-escritos.md`): avisá y ofrecele al abogado dos caminos — **(a) armarlo ahí mismo**, usando la estructura y el articulado estándar del catálogo como base legal, con el estilo que ya conozcas del estudio (pie de firma, tono, por otros escritos que sí tenga modelados); o **(b) que pegue o suba un modelo propio** que tenga a mano (de otra fuente, no necesariamente guardado en el sistema) — en ese caso usalo solo como base de **forma y estilo** para este escrito puntual; el contenido legal sustantivo (articulado, plazos, apercibimientos) seguí sacándolo del catálogo verificado, no de lo que traiga el modelo pegado si difiere. Esto es para este documento puntual del caso — **no lo guardes en `modelos/` como modelo del estudio** a menos que el abogado te lo pida explícitamente.

**Si el tipo de escrito que piden NO está en el catálogo** (ningún tipo de los listados en la `description` se ajusta): no lo improvises ni salgas a buscar en la web para armar un escrito judicial de un tipo que el paquete nunca auditó. Avisá explícitamente que no está cubierto hoy, sugerí que el abogado lo redacte a mano esta vez, y dejalo registrado como señal de producto (mismo criterio que la pregunta de "etapas faltantes" del formulario de alta) — si esto se repite con varios estudios, ahí se justifica investigarlo en serio y sumarlo al catálogo con el mismo rigor que cualquier otra incorporación, no resuelto al vuelo en medio de un caso.

## Paso 3 — Reunir los datos del caso

Pedí los datos que ese escrito necesita (ver el catálogo) y tomá del expediente lo que ya exista en la carpeta del cliente (`clientes/<cliente>/`) o en la conversación. Pedí solo lo que falte.

## Paso 4 — Redactar y guardar

Completá el escrito desde el modelo, respetando el formato local que indique el modelo y el perfil (clave en cédulas y oficios). Entregá el borrador en el chat y guardalo como archivo **nuevo** en la carpeta del cliente (`clientes/<cliente>/`), sin pisar nada.

## Cómo ubicar la carpeta del cliente (antes de guardar)

1. Identificá de qué **cliente / expediente** es la salida. Si no surge claro del contexto, preguntalo (nombre del cliente o carátula).
2. Buscá (Glob) la carpeta de ese cliente dentro de `clientes/`.
3. Si **existe**, guardá ahí. Si **no existe**, creala dentro de `clientes/` y después guardá.
4. Nombrá el archivo de forma descriptiva: `<tipo>-<cliente>-<AAAA-MM-DD>.docx`. Nunca mezcles archivos de distintos clientes ni pises uno existente.

## Nota de verificación

Al terminar, indicá: qué escrito armaste, qué modelo del estudio usaste (o que no había y usaste estructura estándar), qué datos te faltaron, y dónde guardaste el borrador. Es **borrador para revisión y firma del abogado**.

## Conexión con otras skills

Para el **escrito de inicio de ejecución de sentencia**, pedile a **Liquidación de Rubros** el monto actualizado (modo "actualizada") en vez de estimarlo. Para el **segundo traslado / réplica**, si todavía no se hizo el análisis de fondo de la contestación, encadená primero con **Análisis de Contestación**. **No cubre apelación de sentencia** — eso es la skill **Recurso de Apelación**, aunque el usuario diga "recurso" de forma ambigua; si no queda claro cuál de las dos pide, preguntá.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. `perfil_estudio.md` está en `.md` y se lee con `Read` normal. **Los modelos del estudio (todo lo que cuelga de `modelos/`) están en Word `.docx`: extraé su texto con la skill `docx`, nunca con `Read` directo (un `.docx` abierto con `Read` devuelve el binario comprimido, no el texto).** La única salida/insumo que no es `.docx` es la calculadora de liquidación, que es Excel `.xlsx`. Si algún modelo puntual estuviera en `.md`, ese sí se lee con `Read`.
