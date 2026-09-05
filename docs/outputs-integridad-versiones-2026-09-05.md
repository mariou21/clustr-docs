# Outputs: integridad y versiones

Actualización: 5 de septiembre de 2026.

## Guardado y trazabilidad

- El guardado de una nueva versión consulta el registro vigente, conserva una copia independiente de la versión anterior y actualiza la consulta individual con la respuesta confirmada.
- Se evita el doble guardado mientras una operación está en curso. Si ya existe otra versión, se solicita reabrir la cotización antes de sobrescribir. Esto no sustituye un control transaccional entre usuarios que guarden simultáneamente.
- Las revisiones se incrementan por segmentos: después de v.1.9 viene v.1.10.
- Después del primer guardado, nuevas modificaciones en la misma pantalla actualizan esa cotización en lugar de crear otra.
- Se conservan las amenidades del paquete, las opciones de habitación, las condiciones y detalles de actividades, los productos y precios manuales, y las instrucciones de pago.

## Instantáneas históricas

Las cotizaciones guardadas a partir de esta actualización capturan también los datos de presentación del cliente, asesor, configuración PDF y catálogos de vuelo. Al pasar al historial, esos datos se conservan con la versión y no se consultan datos actuales para completarlos.

Las instantáneas antiguas solo pueden mostrar lo que se almacenó: los datos omitidos antes de esta corrección no se reconstruyen retroactivamente ni se sustituyen silenciosamente por datos actuales. Se muestra un aviso cuando falta el contexto histórico. Las imágenes se conservan como referencias a sus archivos, no como copias binarias.

## Correcciones de salidas

- El PDF BETA Editorial ya no recorta las inclusiones a 8 ni las condiciones a 12; la galería utiliza las imágenes guardadas sin el límite global anterior.
- El desglose visual de vuelos contempla cuarta edad; los subtotales por pasajero/noche usan las noches de la habitación. No se modificaron las reglas de cálculo de precios del cotizador.
- PDF y mensajes incluyen las condiciones específicas de paquetes, actividades y vuelos, respetando las secciones habilitadas.
- Los mensajes recorren todos los productos agregados a cada actividad, incluidos precios manuales, y muestran detalles de habitaciones y promociones.
- El motor compartido de correos incluye métodos de pago, condiciones específicas, desglose de pasajeros en vuelos y detalle de productos en actividades.
- Antes de capturar el PDF BETA se espera la versión renderizada y sus datos de vuelo; el correo se prepara desde la misma lectura vigente utilizada para el adjunto. El envío rechaza una versión que cambió durante la preparación.

## Alcance y validación pendiente

Se corrigieron el flujo del cotizador, el historial, el PDF BETA Editorial, los mensajes y el motor compartido de correos. La auditoría exhaustiva de las plantillas PDF heredadas, Compacta y los documentos de origen Asistente queda como una fase separada; no se afirma cobertura completa de esas variantes.

Comprobación técnica realizada sin enviar correos: vista previa de correo generada correctamente, con 25 de 25 métodos de pago y 7 de 7 condiciones de una cotización existente. El guardado y la descarga en navegador deben validarse de extremo a extremo con el Agente de Pruebas.

Objetivos sugeridos: guardar dos revisiones consecutivas y abrir su PDF sin recargar; abrir una versión anterior tras cambiar los datos actuales; generar una salida con paquetes, vuelos, hoteles y múltiples productos de actividad, con secciones activadas y desactivadas.
