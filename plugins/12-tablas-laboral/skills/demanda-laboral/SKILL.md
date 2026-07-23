---
name: demanda-laboral
description: Redacta el escrito de inicio de una demanda laboral (parte trabajadora) adaptado al tipo de caso (despido sin causa, despido indirecto, trabajo no registrado, despido por embarazo/matrimonio, despido durante enfermedad inculpable/reserva de puesto, despido discriminatorio, extinción por fuerza mayor). Vuelca la ficha de primera consulta, el intercambio telegráfico y la documentación del caso, y arma la demanda completa con su liquidación y el ofrecimiento de prueba, a partir del modelo del estudio. Usá esta skill cuando el usuario diga cosas como "armá la demanda", "redactá la demanda laboral", "el escrito de inicio", "demandá a la empresa", "iniciá el juicio". Lee el perfil y el modelo de demanda desde la carpeta del estudio y guarda el borrador en la carpeta del cliente. Borrador para revisión y firma del abogado.
---

# Demanda laboral (parte trabajadora)

Redactá el escrito de inicio adaptado al caso concreto, tomando como base el modelo del estudio y volcando todo el material del expediente. La estructura, los tipos de demanda y los guardrails están en `references/estructura-demanda.md`.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Terminología procesal precisa, redacción formal de escrito judicial (hechos, derecho, petitorio). No agregues advertencias del tipo "esto no es asesoramiento legal".

**Salida única (determinística):** la demanda redactada, mostrada en el chat y guardada como archivo nuevo en la carpeta del cliente. La skill NO presenta el escrito, NO notifica y NO ejecuta ninguna otra acción.

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio (conectada a Cowork, sincronizada con Drive por Google Drive para Escritorio). Encontralo (Glob/Grep por nombre) y tomá su carpeta contenedora como la raíz; buscá `modelos/`, `datos/` y `clientes/` dentro de esa raíz. Tratá todo como sistema de archivos local (Read/Write); no uses el conector/API de Google Drive.

Leé `perfil_estudio.md` y tomá: **jurisdicción y fuero** (define carátula, fuero, organismo, y si el procedimiento admite o no ampliar la demanda), **estilo** de redacción, **jurisprudencia y doctrina de cabecera**, criterio **24.013 vs reparación integral**, y **tasa de interés**. Si no lo encontrás, detené y pedí completar el alta.

## Paso 1 — Identificar el tipo de demanda

Si ya existe una ficha de primera consulta para este cliente, leela primero — probablemente ya tenga resueltas las preguntas de este paso.

**Si no hay ficha (caso de cero):** pedile al abogado el relato general de los hechos —qué pasó, cuándo fue el despido o el hecho principal, motivo, antecedentes relevantes— antes de entrar en las preguntas puntuales de abajo. No clasifiques el tipo solo con respuestas de sí/no sueltas, sin tener también el contexto general del caso.

**Preguntas de diagnóstico obligatorias** (para cualquier caso, tenga o no ficha, si no vienen ya resueltas): ¿estaba en período de prueba?, ¿estaba embarazada o casada/en pareja registrada recientemente y lo notificó fehacientemente?, ¿el despido ocurrió durante una licencia por enfermedad o el período de reserva de puesto?, ¿el empleador invocó alguna causa (disciplinaria, falta o disminución de trabajo, fuerza mayor)? No asumas "no" por silencio. Estas respuestas cambian el tipo, no son un detalle menor.

Con el relato general y estas respuestas, determiná el tipo (ver `references/estructura-demanda.md`): despido sin causa, despido indirecto, trabajo no registrado, despido por embarazo/matrimonio, despido durante enfermedad inculpable/reserva de puesto, despido discriminatorio, o extinción por fuerza mayor. Si no surge claro igual, preguntá.

## Paso 2 — Leer el modelo (carpeta local, solo lectura)

Buscá en `modelos/demandas/` el modelo del **tipo** detectado y leelo. Redactá **por analogía con ese modelo real** (no con una plantilla en blanco): tomá su estructura, sus fórmulas y su forma de fundar. Si no hay un modelo para ese tipo, usá la estructura estándar de `references/estructura-demanda.md` y avisá. No modifiques el modelo.

## Paso 3 — Reunir todo el material del caso

Volcá al escrito todo lo que haya: **ficha de primera consulta** (antigüedad, categoría, CCT, jornada, remuneración, situación registral), **intercambio telegráfico** (intimaciones y respuestas), **documentación** del cliente, datos del trabajador y del empleador, la **jurisdicción/competencia** ya definida (de esa skill o del perfil), y la **liquidación** (tomala de la skill de Liquidación o de `salidas`/carpeta del cliente). Pedí lo que falte; sin la liquidación y los hechos no se cierra.

## Paso 4 — Elegir el modo de redacción

Preguntá siempre, sin excepción: **"¿Redacto la demanda completa de una, o vamos armándola por bloques (hechos → derecho → liquidación → prueba ofrecida → petitorio) y los confirmás antes de armar el documento final?"** Si el perfil del estudio tiene un modo predefinido, mostralo como sugerencia dentro de la misma pregunta (ej: "...tu estudio suele usar 'por bloques', ¿seguimos así o preferís el otro modo para esta demanda?"), pero **nunca lo apliques en silencio sin que el abogado lo confirme para este caso puntual.**

## Paso 5 — Redactar la demanda

Seguí la estructura del modelo y de `references/estructura-demanda.md`. Respetá los **guardrails duros** (aplican en los dos modos):

- **Liquidación completa en la demanda.** Donde el procedimiento de la jurisdicción no admite ampliar, TODO debe estar en el escrito: rubros, prueba y testigos. Lo que no está, no existe.
- **Escala del CCT vigente a la fecha del despido**, NUNCA el salario del telegrama (error que liquida la mitad).
- **Jurisprudencia: poca y aplicable** (tasa de interés, sumas no remunerativas, fallos de cabecera del perfil, CSJN si corresponde). No sobrecargues de doctrina.
- **24.013 vs reparación integral** según el perfil (la reparación integral suele ir como planteo subsidiario, con su fundamentación).

**Modo completo:** redactá el escrito entero de una sola vez —hechos, derecho, liquidación resumida y petitorio integrados según la estructura del modelo— y mostralo completo para revisión.

**Modo por bloques:** redactá y mostrá un bloque a la vez, en este orden, y **no avances al siguiente sin una confirmación explícita del abogado** (silencio o un mensaje ambiguo no cuenta como aprobación — si no queda claro si aprobó o quiere ajustar algo, preguntalo):

1. **Hechos** — el relato fáctico completo, consistente con el material del Paso 3.
2. **Derecho** — el encuadre jurídico aplicable a esos hechos ya confirmados (normativa y jurisprudencia mínima y pertinente).
3. **Liquidación** — los rubros y el cálculo, en dos bloques separados con totales propios (capital directo vs. rubros subsidiarios), conforme `references/estructura-demanda.md`.
4. **Prueba ofrecida** — documental, confesional, testimonial, informativa, pericial y reserva del caso federal, según corresponda (ver `references/estructura-demanda.md`), coherente con los hechos, el derecho y la liquidación ya confirmados.
5. **Petitorio** — coherente con los cuatro bloques anteriores.

Una vez confirmados los cinco bloques, consolidalos en el documento completo con el formato final del modelo — no los pegues sueltos, integralos como un escrito único y coherente — y mostralo entero antes de guardar.

## Paso 6 — Guardar en la carpeta del cliente

Entregá el borrador en el chat y guardalo como archivo nuevo en la carpeta del cliente.

1. Identificá de qué cliente/expediente es; si no surge, preguntá (nombre o carátula).
2. Buscá por nombre la carpeta del cliente dentro de `clientes/`.
3. Si existe, guardá ahí; si no, creala (o pedí que la creen) y guardá.
4. Nombrá el archivo `demanda-<cliente>-<AAAA-MM-DD>.docx`. No pises nada ni mezcles clientes.

## Conexión con otras skills

Usa la **Liquidación** (los rubros) y **Jurisdicción y Competencia** (fuero, carátula, organismo). Después de la demanda, la **Nómina documental / armado del paquete** prepara los adjuntos para la presentación.

## Nota de verificación

Al terminar, indicá: tipo de demanda, qué modelo del estudio usaste (o que no había), qué material del caso integraste y qué te faltó, si la liquidación usó la escala a fecha de despido, **qué modo de redacción se usó (completo o por bloques)**, y dónde guardaste el borrador. Es **borrador para revisión y firma del abogado**.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. Los archivos del cerebro del estudio (`perfil_estudio.md` y todo lo que cuelga de `modelos/`) siguen en `.md` y se leen con `Read` normal.
