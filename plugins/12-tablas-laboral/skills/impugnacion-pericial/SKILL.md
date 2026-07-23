---
name: impugnacion-pericial
description: Redacta el escrito de impugnación o pedido de explicaciones a un dictamen pericial desfavorable en un juicio laboral (parte trabajadora). Caso típico: pericia contable que minimiza o rechaza las diferencias salariales; también pericia médica cuando corresponde (p. ej. enfermedad inculpable, secuelas por violencia laboral). Usá esta skill SIEMPRE que el usuario diga cosas como "impugná la pericia", "impugnación pericial", "la pericia salió en contra", "pedir explicaciones al perito", "impugnar pericia contable / médica", "el perito tomó mal el salario". Lee el perfil del estudio y el modelo de impugnación desde la carpeta del estudio. Genera un borrador de escrito para revisión y firma del abogado.
---

# Impugnación pericial (parte trabajadora)

Redactá el borrador del escrito de impugnación / pedido de explicaciones a un dictamen pericial desfavorable, listo para revisar y firmar, basándote en el perfil y el modelo del estudio. A diferencia de las skills de análisis, esta SÍ produce un escrito para presentar.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Terminología técnica y procesal precisa, fundamentación concreta. No agregues advertencias del tipo "esto no es asesoramiento legal".

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio (conectada a Cowork y sincronizada con Drive por Google Drive para Escritorio). Encontralo (Glob/Grep por nombre) y tomá su **carpeta contenedora como la raíz del estudio**. Todas las demás carpetas — `modelos/`, `datos/` y `clientes/` — están **dentro de esa raíz**: buscalas ahí, nunca como nombres sueltos. Tratá todo como sistema de archivos local: leé con Read y guardá con Write; no uses el conector/API de Google Drive.

Antes de nada, buscá (Glob/Grep) y leé con Read `perfil_estudio.md` en la carpeta del estudio. Tomá: jurisdicción y fuero, criterios de cálculo (incluido el tratamiento de diferencias salariales y tasa), doctrina/fallos de cabecera, estilo y pie de firma. Si no lo encontrás, detené y pedí completar el alta.

## Paso 1 — Leer el modelo (carpeta local, solo lectura)

Buscá por nombre el modelo de impugnación pericial del estudio en `modelos/impugnaciones/`. Tomá de él la estructura, las fórmulas de estilo y el articulado que cita. Si no hay modelo, usá la estructura estándar de un escrito de impugnación. Avisá si trabajaste sin modelo.

## Paso 2 — Reunir el dictamen y el material de contraste

El usuario aporta el **dictamen pericial** (lo pega o adjunta). Reuní además, para contrastar: los **puntos de pericia** ofrecidos, la **liquidación** y la **demanda** (de la carpeta del cliente `clientes/<cliente>/` o del contexto), y la documental relevante. Pedí lo que falte.

## Paso 3 — Detectar los vicios del dictamen

Según el tipo de pericia, buscá errores y omisiones:

- **Contable (diferencias salariales — caso típico):** que el perito haya tomado el salario del telegrama o una escala desactualizada en lugar de la **escala del CCT vigente a la fecha del despido** (error frecuente y costoso); base de cálculo equivocada; horas extras, SAC o adicionales no computados; rubros omitidos; tasa o período mal aplicados; falta de respuesta a puntos de pericia; fundamentación insuficiente; contradicción con recibos/documental.
- **Médica (si corresponde al caso — no cubrimos accidentes/ART):** en disputas por enfermedad inculpable, que la fecha de alta o el diagnóstico no estén respaldados por los estudios, o que no conteste los puntos de pericia sobre la duración de la dolencia; en reclamos por secuelas psicológicas de violencia laboral/mobbing, que no evalúe el nexo con los hechos denunciados o que la metodología no esté fundada.

Listá cada observación con su fundamento técnico y, cuando corresponda, jurídico (perfil del estudio). **Nunca cites un fallo, plenario o doctrina que no hayas podido verificar en el momento** — sin excepción, sin importar cuán segura te "suene" la referencia. Ante la duda, se omite: decilo explícitamente en vez de citar de memoria. Si hace falta investigación jurídica de fondo, derivá o complementá con **Investigación Jurídica**.

## Paso 4 — Redactar el escrito

Redactá la impugnación / pedido de explicaciones siguiendo el modelo: encabezado y carátula, objeto, impugnación punto por punto (cada vicio con su fundamento), pedido concreto (que el perito amplíe o aclare, que se aparte el dictamen, o que se recalcule conforme a derecho), y petitorio. Texto listo para revisar, con el pie de firma del estudio.

Entregá el borrador en la respuesta y guardalo como archivo **nuevo** en la carpeta del cliente, bajo `clientes/<cliente>/`.

## Cómo ubicar la carpeta del cliente (antes de guardar)

1. Identificá de qué **cliente / expediente** es la salida. Si no surge claro del contexto, preguntalo (nombre del cliente o carátula).
2. Buscá (Glob) la carpeta de ese cliente dentro de `clientes/`.
3. Si **existe**, guardá ahí. Si **no existe**, creala dentro de `clientes/` y después guardá.
4. Nombrá el archivo de forma descriptiva: `<tipo>-<cliente>-<AAAA-MM-DD>.docx`. Nunca mezcles archivos de distintos clientes ni pises uno existente.

## Nota de verificación

Al terminar, indicá qué modelo del estudio usaste, si leíste el perfil, qué material de contraste tuviste, y los vicios principales que planteaste. Es **borrador para revisión y firma del abogado**.

## Conexión con otras skills

Se nutre de **Liquidación de Rubros** (para contrastar el cálculo pericial contra el propio) y de la **Demanda** (los puntos de pericia ofrecidos). Si hace falta fundamento jurídico que no esté en el perfil, complementá con **Investigación Jurídica**.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. Los archivos del cerebro del estudio (`perfil_estudio.md` y todo lo que cuelga de `modelos/`) siguen en `.md` y se leen con `Read` normal.
