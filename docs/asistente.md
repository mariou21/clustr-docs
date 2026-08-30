# El Asistente (IA)

## Qué es

Página `/asistente`: compañero de viajes de los agentes. UNA conversación maneja Q&A de
viajes (Haiku + búsqueda web) y creación de COTIZACIONES (Sonnet con salida
estructurada). El catálogo propio siempre va primero ("ventas primero"); los totales se
calculan SIEMPRE en el servidor, nunca en el modelo.

## Entidades

- `AsistenteConfig` — interruptor maestro (`activo`), modelos por lane, tope mensual
  (`cap_usd_mes`), % de aviso, retención (meses), disclosure, precios por Mtok.
- `ChatConversacion` / `ChatMensaje` — hilos por usuario (RLS: cada quien ve lo suyo).
- `ChatUso` — libro de costos: una fila POR llamada, ARMADA antes de gastar
  (`estado pendiente` → `ok`/`error`), con `run_ref` y desglose de tokens.
- `DocCotizacion` — la cotización viva del hilo (datos, faltantes, galería elegida,
  logo del documento, estado borrador/completa).
- `MediaBanco` — banco de imágenes AUTOALIMENTADO: sujeto/tipo (barco, puerto, destino,
  camarote, plano), categoría, fuente y clase de licencia por fila.

## Funciones backend

- `asistente` — la ÚNICA función que llama a la API de Anthropic (Secret
  `ANTHROPIC_API_KEY_ASISTENTE`). Orden por llamada: interruptor → tope → fila de uso
  armada → llamada → costo real registrado. Mezcla automáticamente las Condiciones de
  Configuración aplicables (incl. ventanas de pago por días-hasta-salida).
- `nutrirMediaBanco` — cosecha de fuentes AUTORIZADAS (representación oficial RC /
  Celebrity / Silversea): crucerosroyal.hn, royalcaribbean.com (barco, camarotes por
  categoría, planos de cubierta SVG, puertos), celebritycruises.com y silversea.com
  (fotos del barco). Idempotente, con gate de calidad HTTP y tope de altas por corrida.
- `registrarCotizacion` — convierte una DocCotizacion completa en una Cotización real
  C-### (estado borrador) con snapshot en `historial_versiones`.

## Reglas de dinero

- Tope mensual duro con degradación (modo reducido sin web) y corte (agotado).
- Si no se puede registrar el costo, NO se llama a la API.
- El gasto del mes es visible solo para administradores en la página.

## Documento (Formato B)

Páginas carta fijas: portada foto full-bleed · qué incluye + ficha del barco · La Ruta
(mapa geográfico real + fotos de puertos) · camarotes (foto de la categoría EXACTA o
hueco editable "Agregar foto real de la cabina") · Dónde queda cada cabina (plano
oficial acercado con la cabina enmarcada en rojo; solo si el agente dio cabina) ·
resumen y pagos. UN logo por documento (selector: Travel Diunsa / Royal Caribbean;
cruceros salen con RC). Impresión espera la carga de todas las imágenes.

## Permisos

Módulo `asistente` en grupos (Usuarios → Grupos → "Asistente IA"), apagado por defecto.
