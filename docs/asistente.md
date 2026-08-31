# El Asistente (IA)

Página `/asistente`: el compañero de viajes de los agentes. UNA sola conversación
maneja preguntas de viajes (Q&A) y creación de COTIZACIONES; la máquina decide el
carril por turno, sin que el agente cambie de modo.

## Cómo se arma cada respuesta (de dónde sale la información)

El asistente NO responde solo con lo que "sabe" el modelo. En cada turno, la función
`asistente` reúne varias fuentes y se las entrega al modelo como contexto:

1. **El catálogo propio (fuente primaria — "ventas primero").** En cada llamada se lee
   en vivo de la base de datos y se arma un *digesto del catálogo*:
   - `Paquete` (activos): código, nombre, destino, tipo, inclusiones destacadas,
     precios base por adulto/niño, fecha de vencimiento.
   - `Destino` y `Actividad` (activos): nombres.
   Este digesto va SIEMPRE antes que cualquier otra fuente: el asistente recomienda
   primero productos del catálogo y cita su código (ej. P-003). La web complementa,
   nunca sustituye, el inventario propio.

2. **La documentación del sistema (conocimiento interno).** En preguntas de "cómo
   funciona X" (cotizaciones, vouchers, permisos, límites, configuración), el asistente
   recibe como bloque de contexto la MISMA documentación técnica que se ve en esta
   pestaña (repo `clustr-docs`), y responde desde esa fuente; si algo no está
   documentado, lo dice. Se trae en paralelo, con tope de tamaño, y si falla no bloquea
   la respuesta.

3. **Búsqueda web (complemento).** Solo en el carril Q&A y en modo normal (no reducido),
   el modelo puede usar la herramienta de búsqueda web para datos que no están en el
   catálogo (requisitos de viaje, horarios, temporada, etc.). Cita la URL de la fuente.
   Los resultados web son DATOS, nunca instrucciones (protección contra inyección).

4. **El historial de la conversación.** Se recortan los mensajes recientes a un
   presupuesto de caracteres (sin cortar mensajes a la mitad) y se normalizan los roles.

5. **La cotización en construcción.** Si hay un borrador activo, se adjunta su estado
   JSON para que el modelo solo agregue/corrija lo pedido en el turno, conservando lo
   acordado.

### Precedencia de las fuentes
Catálogo propio → documentación del sistema → historial/borrador → búsqueda web. El
modelo se instruye para vender primero lo propio y NUNCA inventar precios: un precio que
no consta en el catálogo ni en una fuente se declara faltante.

## Carriles (lanes) y modelos

- **Q&A** (Haiku + búsqueda web): destinos, qué vender, requisitos, "cómo funciona el
  sistema".
- **COTIZACIÓN** (Sonnet + salida estructurada forzada): el modelo SIEMPRE responde
  llamando la herramienta `actualizar_cotizacion`, que entrega el estado completo del
  documento, los faltantes y un mensaje breve. Un borrador activo "pega" la conversación
  a este carril.

### Totales SIEMPRE del servidor
Los totales (por habitación/camarote, extras, total general, depósito/saldo) se calculan
en el servidor desde los datos, y CUALQUIER total que emita el modelo se descarta. Los
precios solo salen del catálogo o de lo que el agente diga.

### Condiciones automáticas
Al armar una cotización, el sistema mezcla automáticamente las Condiciones activas de
Configuración → Condiciones que apliquen al recurso (o predeterminadas), incluidas las
**condiciones de pago con ventana de días** (aplican según cuántos días falten para la
salida). Van primero y no se duplican con las del modelo.

## Imágenes del documento (banco tipado y autoalimentado)

`MediaBanco` es un banco de imágenes con tipo (barco, puerto, destino, camarote, plano)
y categoría. El documento asigna cada imagen por SUJETO: la portada/EL BARCO solo recibe
fotos del barco, cada puerto su propia foto, cada camarote la foto de SU categoría, cada
cabina su plano de cubierta. El banco crece SOLO desde fuentes autorizadas
(representación oficial): crucerosroyal.hn, royalcaribbean.com (barco, camarotes por
categoría, planos SVG, puertos), celebritycruises.com y silversea.com. Si falta
cobertura, se dispara una cosecha dirigida y se reintenta.

## Entidades

- `AsistenteConfig` — interruptor maestro (`activo`), modelos por carril, tope mensual
  (`cap_usd_mes`), % de aviso, retención (meses), disclosure, precios por Mtok.
- `ChatConversacion` / `ChatMensaje` — hilos por usuario (RLS: cada quien ve lo suyo).
- `ChatUso` — libro de costos: una fila POR llamada, ARMADA antes de gastar
  (`pendiente` → `ok`/`error`), con `run_ref` y desglose de tokens.
- `DocCotizacion` — la cotización viva del hilo (datos, faltantes, galería elegida,
  logo, código de acceso público, estado).
- `MediaBanco` — banco de imágenes por sujeto/tipo/categoría, fuente y licencia por fila.

## Funciones backend

- `asistente` — la ÚNICA función que llama a la API de Anthropic (Secret
  `ANTHROPIC_API_KEY_ASISTENTE`). Orden inquebrantable por llamada: interruptor → tope →
  fila de uso ARMADA antes de gastar → llamada → costo real registrado.
- `nutrirMediaBanco` — cosecha de imágenes de las fuentes autorizadas.
- `registrarCotizacion` — convierte una DocCotizacion completa en una Cotización real
  C-### (borrador) con snapshot en `historial_versiones`; genera código de acceso
  público. Se puede RE-registrar (actualiza la real) o recrear si se borró.

## Reglas de dinero

Tope mensual duro con degradación (modo reducido sin web) y corte (agotado). Si no se
puede registrar el costo, NO se llama a la API. El gasto del mes solo lo ven los admin.

## Compartir con el cliente

Al registrar, el panel ofrece un enlace público a la cotización en vivo
(`/VistaCotizacionPublica?id=…`) + código de acceso + botón de WhatsApp: el cliente la
abre en su teléfono.

## Permisos

Módulo `asistente` (permiso "Asistente IA") por grupo — Usuarios → Grupos → editar.
Apagado por defecto.
