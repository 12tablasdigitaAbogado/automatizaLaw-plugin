# Catálogo de escritos de trámite

Cada escrito se completa desde su modelo en `modelos/escritos/`. Datos generales que casi todos necesitan: carátula del expediente, juzgado/tribunal y datos de las partes (se toman del expediente en la carpeta del cliente). Abajo, lo propio de cada uno.

## Poder
- **Cuándo:** para acreditar la representación (apud acta o especial), según la práctica del estudio.
- **Datos propios:** datos del trabajador (poderdante) y del letrado (del perfil); objeto del mandato.

## Segundo traslado / réplica a la contestación
- **Cuándo:** corrido el traslado de la contestación (su alcance depende del procedimiento del estudio: amplio o solo de la documental).
- **Datos propios:** la contestación y su documental. Si hace falta el análisis de fondo, usar antes la skill *Análisis de Contestación*; acá se redacta el escrito.

## Pedido de apertura a prueba
- **Cuándo:** para que se abra la causa a prueba.
- **Datos propios:** estado del expediente; prueba ofrecida, si corresponde reiterarla.

## Cédula de notificación
- **Cuándo:** para notificar (de la demanda u otra providencia) cuando la confecciona el estudio.
- **Datos propios:** qué se notifica, destinatario y domicilio, y la oficina/formato que corresponda. El formato cambia por sistema judicial: lo aporta el modelo y el perfil.

## Cédula de prueba (testigos / absolución de posiciones)
- **Cuándo:** para citar testigos o al absolvente, donde corresponda.
- **Datos propios:** identificación de la persona a citar, audiencia y domicilio.

## Oficio (de prueba)
- **Cuándo:** para requerir información o documentación a un organismo.
- **Datos propios:** destinatario del oficio y qué se le pide.

## Acreditación de oficio
- **Cuándo:** para acreditar en el expediente el diligenciamiento de un oficio (típico de los que no admiten vía electrónica).
- **Datos propios:** el oficio diligenciado y la constancia/sello.

## Acuerdo conciliatorio
- **Variantes:** extrajudicial, de homologación directa, o durante el trámite del proceso.
- **Datos propios:** las partes, los rubros y montos acordados, condiciones de pago, y el organismo/sede donde se homologa o registra.

## Escrito de inicio de ejecución de sentencia
- **Cuándo:** firme la sentencia, para ejecutarla.
- **Datos propios:** datos de la sentencia; bienes/cuentas a denunciar si los hay. **El monto a ejecutar (capital actualizado con intereses a la fecha) no lo estimes acá** — pedile a la skill *Liquidación de Rubros* que corra el modo "actualizada" a la fecha de ejecución, y usá esa cifra.

## Recurso (revocatoria / aclaratoria)
- **Cuándo:** contra una providencia o para aclarar/corregir una resolución, según el régimen del estudio. **NO es esto si es una apelación de sentencia** (expresión de agravios) — eso lo cubre la skill *Recurso de Apelación*, no esta.
- **Datos propios:** la resolución recurrida y el agravio o la aclaración pedida.

## Rebeldía
- **Cuándo:** cuando el demandado no contesta la demanda en término.
- **Datos propios:** estado procesal que acredita la falta de contestación.

---

NO pertenecen a esta skill: telegrama / carta documento (skill de Telegrama), demanda (skill de Demanda), apelación de sentencia / expresión de agravios (skill de Recurso de Apelación), y el **pacto de cuota litis** (lo genera la skill de Contrato de Honorarios; acá solo se referencia).
