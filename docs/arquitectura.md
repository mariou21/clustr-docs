# Arquitectura del Proyecto

CLUSTR es una aplicación Base44 (React/Vite) para Travel Diunsa. Este es el mapa
completo de cómo encajan las piezas.

## Planos del sistema

```
  NAVEGADOR DEL AGENTE (travelclustr.com)
  React SPA · Layout + páginas (Cotizaciones, Vouchers, Asistente, Catálogos, …)
        │  llama entidades + funciones vía el SDK de Base44
        ▼
  BASE44 (plataforma / runtime)
  ├─ Entidades (base de datos): Cotizacion, Voucher, Cliente, Paquete, Actividad,
  │     Aerolinea, Destino, GrupoUsuario, ConfiguracionGeneral, Condicion,
  │     ChatConversacion/ChatMensaje/ChatUso/DocCotizacion/MediaBanco/AsistenteConfig …
  ├─ Funciones backend (Deno.serve): asistente · nutrirMediaBanco · registrarCotizacion ·
  │     validarCotizacionPublica · generarPDFCotizacionPublica · enviarCorreo* (Resend) ·
  │     barrido/limpieza* · notificar* · sincronizarDocumentacionGitHub …
  ├─ Secrets: ANTHROPIC_API_KEY_ASISTENTE · GITHUB_PAT · claves de correo …
  └─ Reglas RLS por entidad (p. ej. cada usuario ve sus propios chats/cotizaciones)
        │
        ├─► API de Anthropic (Claude)  — SOLO desde la función `asistente`
        │      Haiku (Q&A + búsqueda web) · Sonnet (cotización, salida estructurada)
        │
        ├─► Sitios oficiales (representación) — cosecha de imágenes de crucero
        │      royalcaribbean.com · celebritycruises.com · silversea.com · crucerosroyal.hn
        │
        └─► Resend (correo) · GitHub (docs) · Supabase (almacenamiento de la plataforma)

  CLIENTE FINAL (teléfono)
  Abre la cotización pública: /VistaCotizacionPublica?id=… + código de acceso
```

## Flujos principales

- **Cotización manual:** el agente arma la cotización en el wizard (`/nuevacotizacion`),
  con secciones Cliente/Paquetes/Alojamientos/Vuelos/Actividades/Resumen/Condiciones/
  Pagos, moneda dual L+USD y control de versiones.
- **Cotización asistida (IA):** en `/asistente`, una conversación arma la cotización; al
  registrarla se convierte en una Cotización real C-###. Ver la sección **Asistente (IA)**.
- **Vouchers:** emisión por tipo de servicio (paquete/alojamiento/actividad/traslado),
  con plantilla PDF propia.
- **Publicación al cliente:** cotización compartible por enlace público + código de
  acceso; opcionalmente por correo (Resend) o WhatsApp.
- **Catálogos y configuración:** paquetes, actividades, destinos, inclusiones,
  condiciones, métodos de pago, plantillas de correo/PDF, permisos por grupo.

## Cómo se construye y se opera el proyecto (fuera del runtime)

El código vive en GitHub (`mariou21/Clustr`) y la documentación en `mariou21/clustr-docs`.
El desarrollo se hace en una estación de trabajo (Tower) con Claude Code: allí se edita,
se corren las compuertas (build, tests, lint, verificación de que la llave nunca viaja en
el bundle) y se automatiza el navegador para publicar. Base44 sincroniza desde GitHub y
la publicación deja la app en vivo. **El runtime del chatbot y de la app NO corre en la
estación de trabajo — corre en Base44 + Anthropic + los sitios externos.** (Diagrama
detallado del rol de la estación de trabajo: entregado aparte.)

## Principios

- **Ventas primero:** el catálogo propio manda sobre la web.
- **Honestidad de costos:** el gasto se registra antes de gastar; sin registro, no hay
  llamada.
- **Nunca inventar:** precios/planos/imágenes solo de fuentes reales; si falta, se
  declara faltante o se deja un hueco editable.
- **RLS + permisos por grupo:** cada agente ve lo suyo; los módulos se habilitan por
  grupo.
