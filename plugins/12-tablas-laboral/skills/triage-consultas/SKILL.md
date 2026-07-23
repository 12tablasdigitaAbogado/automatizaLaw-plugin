---
name: triage-consultas
description: Hace el triage de una consulta laboral nueva (parte trabajadora) antes de tomar el caso: aplica los filtros de viabilidad del estudio y devuelve una recomendación de continuar / descartar / derivar, con el motivo. Usá esta skill SIEMPRE que el usuario diga cosas como "¿tomo este caso?", "¿es viable esta consulta?", "filtrá esta consulta", "triage", "¿es potable este cliente?", "me consultó un trabajador, ¿sigo o descarto?". Lee los filtros del estudio desde el perfil en la carpeta del estudio. Es una recomendación interna para el abogado.
---

# Triage de consultas (parte trabajadora)

Evaluá una consulta laboral nueva contra los filtros de viabilidad del estudio y devolvé una recomendación clara: **continuar / descartar / derivar**, con el motivo. Es una decisión asistida para el abogado, no un dictamen definitivo.

Sos asistente de un estudio jurídico laboral argentino que representa al **trabajador (parte actora)**. Directo, con criterio. No agregues advertencias del tipo "esto no es asesoramiento legal".

## Paso 0 — Leer el perfil del estudio (carpeta local)

**Anclaje (raíz del estudio):** `perfil_estudio.md` es único en la carpeta del estudio (conectada a Cowork y sincronizada con Drive por Google Drive para Escritorio). Encontralo (Glob/Grep por nombre) y tomá su **carpeta contenedora como la raíz del estudio**. Todas las demás carpetas — `modelos/`, `datos/` y `clientes/` — están **dentro de esa raíz**: buscalas ahí, nunca como nombres sueltos. Tratá todo como sistema de archivos local: leé con Read y guardá con Write; no uses el conector/API de Google Drive.

Antes de nada, buscá (Glob/Grep) y leé con Read `perfil_estudio.md` en la carpeta del estudio. De ahí salen **los filtros de toma de ese estudio** (su nicho y sus criterios), que son los que tenés que aplicar. Pueden incluir, según el estudio: tipo de relación (privada vs estatal/pública), prescripción (p. ej. 2 años desde el despido), zonas geográficas que cubre, actividades que NO toma (agraria, construcción, doméstico, etc.), antigüedad y salario mínimos (nichos de salario alto), situación registral, y que no sea una causa ya iniciada por otro abogado. Si no encontrás el perfil, detené y pedí completar el alta (sin los filtros del estudio no podés decidir bien).

## Paso 1 — Pedir los datos del caso

Antes de pedir nada, buscá (Glob/Grep) en `clientes/<cliente>/` si ya existe una **ficha de primera consulta** guardada para este caso. Si existe, tomá los datos de ahí (incluidos los que haya marcado como `PENDIENTE`) en vez de volver a preguntarlos desde cero — solo pedí lo que falte o siga pendiente.

Pedí al usuario solo los datos que requieren los filtros del perfil. Habitualmente: tipo de empleador (privado/público), fecha de despido o de los hechos (para prescripción), antigüedad, remuneración aproximada, actividad/sector, situación registral (registrado / mal registrado / no registrado), lugar de trabajo (zona), y si ya intervino otro abogado. Si el relato vino libre (audio/WhatsApp), extraé de ahí lo que puedas y preguntá solo lo que falte.

## Paso 2 — Aplicar los filtros y decidir

Cotejá cada dato contra los filtros del perfil. Devolvé:

- **Recomendación: continuar / descartar / derivar.**
- **Motivo por filtro**: qué filtros pasa y cuáles no (p. ej. "prescripto: el despido fue hace más de 2 años → descartar"; "relación estatal → fuera del nicho → derivar").
- Si hay un dato dudoso o faltante que cambia la decisión, marcalo como **semáforo amarillo** y decí qué habría que confirmar.
- Si la recomendación es **continuar**, sugerí el próximo paso del estudio (p. ej. citar a consulta presencial y qué documentación pedir según la situación registral).

## Paso 3 — Entregar

Mostrá la recomendación con su fundamento, breve y accionable. La decisión final es del abogado.

## Conexión con otras skills

Se nutre de la **ficha de primera consulta** si ya existe (ver Paso 1). Si todavía no hay ficha y la recomendación es continuar, encadená con ella antes de seguir. Si el estudio opera en más de una provincia, encadená también con **Jurisdicción y Competencia**.

## Nota de verificación

Al terminar, indicá qué filtros del perfil aplicaste y qué datos te faltaron. Es una recomendación interna; la toma de la causa la decide el abogado.

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. `perfil_estudio.md` está en `.md` y se lee con `Read` normal. **Los modelos del estudio (todo lo que cuelga de `modelos/`) están en Word `.docx`: extraé su texto con la skill `docx`, nunca con `Read` directo (un `.docx` abierto con `Read` devuelve el binario comprimido, no el texto).** La única salida/insumo que no es `.docx` es la calculadora de liquidación, que es Excel `.xlsx`. Si algún modelo puntual estuviera en `.md`, ese sí se lee con `Read`.
