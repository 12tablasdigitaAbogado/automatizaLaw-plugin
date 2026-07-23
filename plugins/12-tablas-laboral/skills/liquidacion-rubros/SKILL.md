---
name: liquidacion-rubros
description: Calcula la liquidación final e indemnizatoria de un despido laboral (parte trabajadora) generando una planilla Excel con fórmulas, donde la cuenta la hace Excel y no el modelo. Cubre el núcleo indemnizatorio (antigüedad art. 245 con tope y Vizzoti, preaviso, integración, SAC, vacaciones, días trabajados), las multas según el criterio del estudio, las diferencias salariales, y los rubros de embarazo/matrimonio (art. 182 LCT), enfermedad inculpable/reserva de puesto (arts. 208-213 LCT) y fuerza mayor (art. 247 LCT) cuando el caso corresponde. Usá esta skill SIEMPRE que el usuario diga cosas como "liquidá", "armá la liquidación", "calculá la indemnización", "liquidación por despido", "cuánto le corresponde", "planilla de liquidación", "diferencias salariales". Lee el perfil y la planilla del estudio desde la carpeta del estudio. Genera un Excel nuevo, borrador para revisión del abogado.
---

# Liquidación de rubros (parte trabajadora)

Generá la liquidación como **planilla de Excel con fórmulas**: los importes se calculan en las celdas, no los estima el modelo. Tu trabajo es juntar los datos, aplicar los criterios del estudio y armar la planilla; **la aritmética la hace Excel**.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Preciso, ordenado. No agregues advertencias del tipo "esto no es asesoramiento legal".

## Dónde vive el estudio (carpeta local sincronizada)

El estudio trabaja sobre una **carpeta conectada a Cowork** (el "cerebro": `perfil_estudio.md` + `modelos/` + `datos/` + `clientes/`). Esa carpeta está sincronizada con Google Drive por Google Drive para Escritorio, pero vos la tratás como **sistema de archivos local**: leé con Read y guardá con Write. No uses el conector/API de Google Drive para leer ni para escribir.

## Reglas duras (no negociar)

- **El modelo no hace cuentas de cabeza.** Toda operación va como fórmula en la planilla Excel (usá la skill `xlsx`). Mostrá inputs y resultados por separado.
- **Solo lectura sobre lo existente; siempre archivo nuevo, en la carpeta del cliente.** Leé el perfil y la plantilla del estudio sin modificarlos. Generá un Excel **nuevo** y guardalo (Write) en la carpeta del cliente (`clientes/<cliente>/`), nunca en una carpeta común ni pisando un archivo existente.
- **Escala a fecha de despido, nunca inventada.** Para diferencias salariales y para el tope del art. 245 usá la **escala del CCT vigente a la fecha del despido** (NUNCA el salario del telegrama, NUNCA la escala más reciente si el despido fue en el pasado). Buscala en `datos/escalas-cct/`; si no está, en la web para esa fecha puntual, citando la fuente; si no la encontrás verificada, pedísela al abogado — nunca la estimes.
- **Rubros derogados NUNCA en el capital directo.** Las multas de las leyes 24.013 y 25.323 (arts. 1 y 2), la **multa del art. 80 LCT** (3 remuneraciones) y la **reparación integral** van SIEMPRE en el bloque **«rubros subsidiarios»** de la planilla (subtotal propio), **nunca sumados al TOTAL de capital directo**. Por defecto van **apagados**; sólo se activan como subsidiarios (planteo de inconstitucionalidad) si el caso lo amerita. El monto del OBJETO/petitorio se expresa como **capital directo** y, en subsidio, los subsidiarios.
- **Borrador.** El resultado lo revisa y valida el abogado.

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio. Encontralo (Glob/Grep por nombre dentro de la carpeta conectada) y tomá su **carpeta contenedora como la raíz del estudio**. Todas las demás carpetas — `modelos/`, `datos/` y `clientes/` — están **dentro de esa raíz**: buscalas ahí, nunca como nombres sueltos.

Leé `perfil_estudio.md` con Read. Tomá los criterios de cálculo del estudio: qué **rubros** liquida, qué **multas** aplica (varía por estudio), tratamiento del **tope del art. 245** (corrección *Vizzoti* — ya legislada expresamente por la Ley 27.802, no solo doctrina CSJN opcional; aplicala por default si la matemática lo amerita), **actualización/tasa** y fecha de cálculo. Si no encontrás el perfil, detené y pedí conectar la carpeta del estudio / completar el alta.

**Marco normativo vigente (Ley 27.802, Modernización Laboral, vig. 6/3/2026):** el núcleo indemnizatorio (arts. 232, 233, 245, 156) **no cambió**. Lo que sí cambió: (a) **actualización** de créditos por **IPC-INDEC + 3% anual** para causas nuevas (nuevo **art. 276 LCT**) — reemplaza la tasa activa BNA / actas CNAT; (b) las **multas** por registración (leyes 24.013 y 25.323 arts. 1 y 2) y la **multa del art. 80 LCT** (3 sueldos) están **derogadas** (Ley 27.742, mantenido por la 27.802) → van **apagadas**; la registración deficiente se **remite a ARCA** (art. 278) y el reclamo del trabajador por la clandestinidad va por **reparación integral / inconstitucionalidad** (criterio del estudio, rubro subsidiario); (c) el **FAL** no reduce el crédito del trabajador (art. 58) — el art. 245 se reclama íntegro salvo que un CCT haya adoptado el FAL como reemplazo total (excepcional). Confirmá siempre el marco vigente a la fecha del despido.

## Paso 1 — Tomar la plantilla del estudio (solo lectura)

Buscá la **calculadora modelo** del estudio en `modelos/liquidaciones/` (un Excel con las fórmulas ya armadas y celdas de input) y abrila con la skill `xlsx` (es Excel `.xlsx`, no uses `Read` directo). Esa es la base; **no la modifiques**. Si no estuviera, usá como respaldo la estructura y las fórmulas de `references/formulas-liquidacion.md`.

## Paso 2 — Pedir los datos del caso

Pedí en una sola tanda: fecha de ingreso y de despido (→ antigüedad), **mejor remuneración mensual normal y habitual** (base art. 245), CCT aplicable y su **tope**, si hubo o no preaviso, si el despido cae a mitad de mes (integración), remuneraciones del semestre (SAC), vacaciones pendientes, haberes del mes adeudados, y qué rubros/multas incluir (por defecto, los del perfil). Si el tipo de caso (de la ficha de primera consulta o de `demanda-laboral`) es alguno de estos, pedí además el dato específico: **embarazo/matrimonio** → fecha de notificación fehaciente; **enfermedad inculpable/reserva de puesto** → fecha de alta médica o de vencimiento de la reserva; **fuerza mayor** → si el empleador invocó la causal formalmente. Para **diferencias salariales** y para el **tope del art. 245**, necesitás la escala del CCT aplicable **vigente a la fecha del despido** (no la más reciente si el despido fue en el pasado — la prescripción permite reclamos de hasta 2 años atrás). Buscala en este orden: (1) `datos/escalas-cct/`; (2) si no está ahí, buscala en la web, puntualmente para esa fecha, y citá la fuente (paritaria, boletín oficial, o el sitio del sindicato/cámara empresaria); (3) si no la encontrás verificada por ninguna de las dos vías, **pedísela al abogado** — nunca estimes ni uses una escala de otra fecha "aproximando". Lo mismo con lo efectivamente percibido mes a mes: eso lo aporta el caso, no se busca.

## Paso 3 — Construir la planilla (Excel con fórmulas)

Hacé una **copia** de la calculadora modelo y completá solo sus **celdas de input** con los datos del caso y los criterios del perfil (activá las multas únicamente si corresponde según el perfil y la fecha de despido). La copia mantiene las fórmulas: **la cuenta la hace Excel**, no la estimás vos. Si tuviste que armarla desde el respaldo (`references/formulas-liquidacion.md`), incluí una hoja de datos, una de liquidación con fórmulas y los totales. Contemplá los modos que pida el usuario:

- **Preliminar** (estimación de viabilidad), **Definitiva para demanda** (completa), o **Actualizada** (aplicando la tasa de interés del perfil a la fecha indicada).
- Núcleo: antigüedad (245 con tope/Vizzoti — aplicá Vizzoti por default si la matemática lo amerita, no solo si el perfil lo tiene activado), preaviso (232) + SAC, integración (233) + SAC, SAC proporcional, vacaciones no gozadas (156), días trabajados.
- **Embarazo/matrimonio, enfermedad inculpable/reserva de puesto, o fuerza mayor**: si el tipo de caso corresponde a alguno de estos, activá el rubro respectivo (`references/formulas-liquidacion.md`, secciones 9 a 11) — se suman a (o, en fuerza mayor, reemplazan parcialmente) las indemnizaciones comunes, no van por separado sin conexión con el resto.
- Multas: para extinciones desde el 9/7/2024, las de las leyes 24.013 y 25.323 (arts. 1 y 2) y la del art. 80 LCT están **derogadas** (Ley 27.742 / 27.802) → **apagadas**. Si el estudio reclama por la clandestinidad, usá el rubro **reparación integral** (monto a fijar por el abogado) y/o segregá las multas como **subsidiarias** sujetas a planteo de inconstitucionalidad. Nunca las sumes al capital directo.
- Actualización (modo Actualizada): IPC-INDEC + 3% anual (art. 276 LCT) para causas nuevas; no uses tasa activa BNA salvo que el perfil lo indique para un caso en trámite.
- Diferencias salariales (si aplica): hoja aparte, mes a mes, escala CCT vigente a fecha de despido vs percibido.

## Paso 4 — Entregar

Guardá el Excel nuevo con Write en la carpeta del cliente (`clientes/<cliente>/`). **Presentá el archivo** al usuario. Mostrá además un resumen de los rubros y el total, y aclarará qué criterios del perfil aplicaste.

## Cómo ubicar la carpeta del cliente (antes de guardar)

1. Identificá de qué **cliente / expediente** es la salida. Si no surge claro del contexto, preguntalo (nombre del cliente o carátula).
2. Buscá (Glob) la carpeta de ese cliente dentro de `clientes/` en la raíz del estudio.
3. Si **existe**, guardá ahí. Si **no existe**, creala dentro de `clientes/` y después guardá.
4. Nombrá el archivo de forma descriptiva: `<tipo>-<cliente>-<AAAA-MM-DD>.xlsx`. Nunca mezcles archivos de distintos clientes ni pises uno existente.

## Nota de verificación

Al terminar, indicá: qué perfil y qué plantilla usaste, qué criterios aplicaste (tope/Vizzoti, multas o reparación integral, tasa), y si las diferencias salariales se calcularon con la escala a fecha de despido. Es **borrador para revisión y validación del abogado**.

## Referencia

Las fórmulas exactas de cada rubro están en `references/formulas-liquidacion.md`.

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. `perfil_estudio.md` está en `.md` y se lee con `Read` normal. **Los modelos del estudio (todo lo que cuelga de `modelos/`) están en Word `.docx`: extraé su texto con la skill `docx`, nunca con `Read` directo (un `.docx` abierto con `Read` devuelve el binario comprimido, no el texto).** La única salida/insumo que no es `.docx` es la calculadora de liquidación, que es Excel `.xlsx`. Si algún modelo puntual estuviera en `.md`, ese sí se lee con `Read`.
