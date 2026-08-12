# Funciones Backend

## validarCotizacionPublica

**Propósito:** Validar un código de acceso público y devolver cotización, cliente y configuración para la vista pública.

**Entrada:**

```
{ "codigo_acceso": "string" }
```

**Respuesta:** Retorna `cotizacion`, `cliente` y `config` usando acceso de servicio.

---

## Envío de correos y documentos

**enviarCotizacionPDF**
Envía la cotización por correo con adjunto PDF configurable desde Plantillas, con versión independiente de la descarga y control separado de plantilla, secciones, márgenes y estilos.

**enviarCorreoResend**
Envía correos de cotización mediante Resend con remitente configurable y adjuntos base64 opcionales.

**enviarCorreoVoucher**
Envía vouchers por correo usando la plantilla de voucher y adjunto PDF generado desde la misma vista visual para conservar la composición del documento.

---

## Mantenimiento y automatizaciones

- **limpiarPapelera:** elimina registros en papelera que superan los días de retención configurados.
- **verificarCotizacionesVencidas:** actualiza cotizaciones pendientes a vencido según fecha de validez.
- **procesarNotificaciones:** crea notificaciones automáticas según reglas activas en ConfiguracionNotificacion.

**Automatizaciones activas documentadas:**

- Programada para verificar cotizaciones vencidas diariamente
- Programada para procesar notificaciones de forma recurrente
- Automatizaciones por entidad para eliminación en cascada de catálogos relacionados
