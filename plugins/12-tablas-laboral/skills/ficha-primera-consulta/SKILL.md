---
name: ficha-primera-consulta
description: >-
  Estructura la ficha de primera consulta de un trabajador (parte actora) antes del
  triage: datos del trabajador y del empleador, relación laboral, motivo de la
  consulta, fecha de los hechos (para prescripción), documentación que ya aporta, y
  las preguntas de diagnóstico que después necesitan las demás skills (período de
  prueba, embarazo/matrimonio, licencia por enfermedad o reserva de puesto, causal
  invocada por el empleador). Usá esta skill cuando el usuario diga cosas como "armá
  la ficha de primera consulta", "tomá nota de esta consulta", "cargá los datos de
  este cliente nuevo", "primera entrevista", "intake del cliente", o cuando pegue el
  relato/notas de una consulta nueva antes de pedir el triage. No decide viabilidad
  (eso es `triage-consultas`) ni redacta nada — es el insumo de datos crudos para
  todo lo que sigue.
---

# Ficha de primera consulta (parte trabajadora)

Estructurás la información de la primera consulta de un trabajador que puede convertirse en cliente. Sos el punto de entrada de datos de todo el proceso: lo que quede mal cargado o sin preguntar acá se lo va a comer cada skill que venga después.

**Salida:** una ficha estructurada, mostrada en el chat y guardada en la carpeta del cliente. No decidís si el caso es viable (eso lo hace `triage-consultas` con esta ficha como insumo) ni redactás nada todavía.

## Paso 0 — Leer el perfil del estudio

Buscá y leé `perfil_estudio.md` en la carpeta del estudio (Glob/Grep por nombre, tomá su carpeta contenedora como raíz; `clientes/` cuelga de ahí). Tomalo por si el estudio pide algún dato adicional propio de su práctica (además de los de este checklist). Si no lo encontrás, seguí igual con el checklist estándar y avisá que trabajaste sin perfil.

## Paso 1 — Identificar al cliente y crear/ubicar su carpeta

Si es un cliente nuevo, determiná el nombre para la carpeta (`clientes/<nombre-apellido>/`) y creala si no existe. Si ya existe una consulta previa de la misma persona, avisá — no dupliques la ficha, actualizá o preguntá si es un caso distinto.

## Paso 2 — Cargar el checklist con lo que el usuario ya aportó

Tomá el relato, notas o transcripción que te pasen y completá el checklist de abajo con lo que surja. **No inventes ni asumas nada que no esté dicho** — todo campo sin dato queda como `PENDIENTE`, nunca se completa por defecto (ni con "no", ni con "no aplica", ni con un valor típico).

### A. Trabajador
Nombre completo, DNI, domicilio, teléfono, email, fecha de nacimiento.

### B. Empleador
Razón social o nombre, CUIT (si lo tiene), domicilio, actividad, CCT aplicable (si se conoce).

### C. Relación laboral
Fecha de ingreso, categoría/puesto, jornada, remuneración (básico y cómo se pagaba: en blanco, en negro, mixto), ¿estaba correctamente registrado? (si no, detalle de la sub-registración: qué parte no figuraba), CCT que se le aplicaba en los hechos.

### D. Motivo de la consulta y fecha de los hechos
Qué pasó, en las palabras del trabajador. **Fecha exacta o aproximada del hecho principal** (despido, último día trabajado, hecho que motiva el reclamo) — es el dato que define la prescripción (2 años, art. 256 LCT); si ya pasaron más de 2 años o está cerca del límite, marcalo como alerta destacada, no lo dejes perdido en el texto. ¿La relación laboral sigue vigente o ya se desvinculó?

### E. Preguntas de diagnóstico (obligatorias — de esto depende cómo se clasifique el caso más adelante)

Preguntá explícitamente, no asumas por default "no" ante el silencio:

- ¿Estaba en período de prueba al momento del hecho?
- ¿Estaba embarazada, o casada/en pareja registrada recientemente, y lo notificó fehacientemente al empleador?
- ¿Estaba de licencia por enfermedad o dentro del período de reserva de puesto (arts. 208-213 LCT) al momento del despido?
- ¿El empleador invocó una causa? ¿Cuál? (causal disciplinaria, falta o disminución de trabajo, fuerza mayor, u otra)
- ¿Hubo hechos de hostigamiento, violencia laboral o discriminación además del despido en sí?
- ¿Ya hubo intercambio telegráfico (CD/TCL) entre las partes? Si sí, pedí que lo aporte — no lo reconstruyas de memoria.

### F. Documentación que el cliente ya aporta

Listá lo que efectivamente trajo o mencionó tener (recibos, contrato, certificados, capturas de mensajes, telegramas, etc.), diferenciando de lo que dijo que "puede conseguir" pero todavía no tiene.

### G. Observaciones libres

Cualquier dato relevante que no encaje en las categorías anteriores (relato del cliente en sus palabras, contexto, tono de la consulta).

## Paso 3 — Señalar lo que falta

Al final del checklist, un bloque aparte: **"Pendiente de confirmar"** con la lista de todos los campos que quedaron en `PENDIENTE`, especialmente los del punto E — son los que más cambian la clasificación posterior. No se los "complete" en la próxima consulta si no se los vuelve a preguntar explícitamente.

## Guardrails duros (no negociar)

- **Nunca completes un campo por default.** Silencio no es "no" — es dato faltante.
- **La fecha del hecho principal siempre se destaca aparte**, con el cálculo de cuánto falta para los 2 años de prescripción (o si ya se cumplió).
- **No calcules viabilidad ni digas "conviene tomar este caso".** Eso es `triage-consultas`.
- **No redactes nada** (ni telegrama, ni demanda) — esta skill solo estructura datos.

## Conexión con otras skills

Esta ficha es el insumo de entrada de **Triage de Consultas** (viabilidad), **Demanda Laboral** (usa directamente las respuestas del punto E para clasificar el tipo, sin volver a preguntarlas), **Telegrama/Carta Documento** (qué intimación corresponde según el motivo de consulta) y **Jurisdicción y Competencia** (domicilios y lugar de tareas ya capturados en A/B/C). Guardala siempre en la carpeta del cliente antes de pasar a cualquiera de esas skills.

## Nota de verificación

Al terminar, indicá: qué campos quedaron completos, cuáles en `PENDIENTE` (con foco en los del punto E), si pudiste leer el perfil del estudio, y el estado de la prescripción calculado sobre la fecha del hecho principal. Es una ficha de datos crudos para uso interno del estudio — no es un documento para el cliente ni un dictamen sobre el caso.
