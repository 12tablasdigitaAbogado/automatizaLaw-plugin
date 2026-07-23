---
name: recurso-apelacion
description: >-
  Redacta la expresión de agravios (memorial de apelación) contra una sentencia de
  primera instancia adversa o parcialmente adversa, parte trabajadora. Identifica
  cada punto agraviante de la sentencia, lo funda con crítica concreta y razonada
  (requisito procesal — sin esto la Cámara puede declarar desierto el recurso) contra
  la prueba realmente producida y la normativa aplicable, citando jurisprudencia
  solo si puede verificarla. Usá esta skill cuando el usuario diga cosas como "armá
  la expresión de agravios", "apelá la sentencia", "vamos a apelar", "la sentencia
  salió en contra, ¿qué hacemos?", "memorial de agravios", "recurramos el fallo". No
  cubre revocatoria ni aclaratoria (eso es Escritos de Trámite) ni recurso
  extraordinario ante tribunales superiores.
---

# Recurso de apelación / expresión de agravios (parte trabajadora)

Redactás la expresión de agravios contra una sentencia de primera instancia que resultó adversa, total o parcialmente, para el trabajador. Es la pieza que sostiene toda la apelación — si la crítica no es concreta y razonada sobre cada punto, el recurso puede caer por defecto de forma, sin que la Cámara llegue a mirar el fondo.

**Salida:** borrador de expresión de agravios para revisión y firma del abogado, guardado en la carpeta del cliente.

## Paso 0 — Leer el perfil y reunir el expediente

Leé `perfil_estudio.md` (jurisdicción, fallos de cabecera) y buscá en `clientes/<cliente>/` la sentencia, la demanda, la contestación, y la prueba producida (pericias, testimonial, documental). **No armes ningún agravio sobre una prueba o un hecho que no esté efectivamente en el expediente** — si falta algo para fundar un punto, pedilo antes de inventar el contenido.

## Paso 1 — Leer el modelo (carpeta local, solo lectura)

Buscá en `modelos/escritos/` el modelo de expresión de agravios del estudio (por palabra clave) y leelo: tomá su estructura, estilo de fundamentación y forma de organizar los agravios. Si no hay un modelo para esto, usá la estructura estándar del Paso 4 y avisá. No modifiques el modelo.

## Paso 2 — Identificar cada punto agraviante

Comparado lo pedido en la demanda contra lo resuelto en la sentencia, listá cada punto donde el trabajador sale perjudicado: rubro rechazado o reducido, antigüedad mal computada, categoría no reconocida, prueba mal valorada o ignorada, aplicación incorrecta de una norma, tasa de interés mal fijada, costas impuestas en contra, u otro. Cada punto agraviante es un agravio separado — no los mezcles en un reclamo genérico.

## Paso 3 — Fundar cada agravio con crítica concreta y razonada

Para cada agravio, armá:

- **Qué dijo exactamente la sentencia** en ese punto (citá el considerando).
- **Por qué está mal**, con referencia concreta a la prueba del expediente que la sentencia no consideró o valoró mal, y/o al artículo de ley aplicado incorrectamente. Esto tiene que ser específico — "el juez se equivocó" no alcanza; tiene que decir qué prueba ignoró, qué norma aplicó mal, y por qué la conclusión correcta es otra.
- **Jurisprudencia o doctrina — solo si la podés verificar ahora**, con la misma regla que en toda consulta de fondo del paquete: buscá antes de citar (mismo criterio que `investigacion-juridica`); si no encontrás algo verificable para ese punto puntual, decilo así en vez de citar de memoria o generalizar.
- **Qué le pedís a la Cámara** respecto de ese punto (que revoque, que modifique el monto a tal cifra —si es un rubro numérico, pedile el número exacto a `liquidacion-rubros` en vez de estimarlo—, que reconozca tal hecho).

## Paso 4 — Armar la pieza completa

Seguí la estructura del modelo del estudio si lo encontraste en el Paso 1; si no había, usá esta estructura habitual: (1) objeto (apela la sentencia de fecha X, expresa agravios), (2) antecedentes breves del proceso, (3) cada agravio numerado con su fundamento (Paso 3), (4) petitorio concreto punto por punto, (5) petitorio final (que se revoque/modifique la sentencia conforme a lo expuesto, con costas).

## Guardrails duros (no negociar)

- **Cada agravio necesita crítica concreta y razonada — nunca una disconformidad genérica.** Es un requisito procesal, no una preferencia de estilo: si falta, la Cámara puede declarar el recurso desierto y el agravio se pierde sin que se lo mire.
- **No arames ningún agravio sobre prueba o hechos que no estén en el expediente real.** Si falta un dato para fundar un punto, pedilo antes de asumir cómo habría sido esa prueba.
- **Nunca citá jurisprudencia o doctrina que no hayas verificado en el momento.** Sin excepción, aunque suene plausible.
- **Verificá el plazo para expresar agravios de esa jurisdicción antes de asumir uno** — varía según el fuero y el tipo de procedimiento (ordinario vs. abreviado); coordiná con `plazos-procesales` en vez de asumir un número.
- **Si un agravio es sobre un monto, pedí la cifra exacta a `liquidacion-rubros`** — no estimes un número por tu cuenta.

## Conexión con otras skills

Se nutre de la sentencia, la demanda y la prueba producida (expediente del cliente), de **Investigación Jurídica** para la jurisprudencia de Cámara verificada, y de **Liquidación de Rubros** si algún agravio es sobre un monto. Coordiná con **Plazos Procesales** para el vencimiento del plazo de apelación. No reemplaza a **Escritos de Trámite** (revocatoria/aclaratoria) ni cubre recurso extraordinario.

## Nota de verificación

Al terminar, indicá: cuántos agravios identificaste y sobre qué expediente/prueba los fundaste, qué jurisprudencia buscaste y si encontraste algo verificable para cada punto (o no), y que el plazo de presentación queda pendiente de confirmar en la jurisdicción concreta del caso. Es un borrador para revisión y firma del abogado, no una pieza lista para presentar sin control.

## Formato del archivo de salida (Word .docx)

El archivo que guardás en la carpeta del cliente va **siempre en Word (`.docx`)**, nunca en `.md` ni en texto plano. Generá el `.docx` con la skill `docx` a partir del texto ya redactado, respetando el formato del escrito (encabezado, cuerpo, firma). El nombre del archivo lleva la extensión `.docx`. Como la carpeta del estudio está sincronizada con Google Drive, el `.docx` queda disponible ahí y el abogado lo abre y edita directamente en Google Docs. (La única salida del plugin que no es `.docx` es la liquidación, que es una planilla Excel.)

## Lectura de documentos ya generados (Word .docx)

Los documentos que el estudio ya generó y guardó antes en `clientes/<cliente>/` (ficha, demanda, análisis de contestación, escritos, etc.) están en Word (`.docx`). Para leer su contenido, extraé el texto con la skill `docx`; **no uses `Read` directo sobre un `.docx`**, porque devuelve el binario comprimido y no el texto legible. Los archivos del cerebro del estudio (`perfil_estudio.md` y todo lo que cuelga de `modelos/`) siguen en `.md` y se leen con `Read` normal.
