# Notificaciones y Recordatorios

## Sistema de Notificaciones

El sistema implementa un mecanismo completo de notificaciones in-app para mantener a los agentes informados sobre eventos importantes.

**Componentes del Sistema:**

- **Entidad Notificacion:** Almacena todas las notificaciones con estado leída/no leída
- **NotificacionesBell:** Componente campana en header con contador de no leídas
- **Función Backend procesarNotificaciones:** Genera notificaciones automáticas según eventos del sistema
- **Actualizaciones en tiempo real:** Las notificaciones se refrescan cada 60 segundos automáticamente

**Características:**

- Indicador visual en campana con número de notificaciones no leídas
- Popover con lista completa de notificaciones
- Iconos y colores según tipo de notificación
- Marcado individual o masivo de notificaciones como leídas
- Navegación directa a la entidad relacionada
- Eliminación de notificaciones antiguas o irrelevantes
- Scroll vertical en lista larga de notificaciones

---

## Notificaciones Automáticas

Las notificaciones se generan automáticamente mediante la función `procesarNotificaciones` que debe ejecutarse periódicamente (recomendado: cada hora o mediante cronjob).

### 1. Cotizaciones Próximas a Vencer

- **Trigger:** Cotización en estado "pendiente" a 2 días de su fecha_validez
- **Destinatario:** Usuario creador de la cotización (created_by)
- **Mensaje:** "La cotización {codigo} vence en 2 días ({fecha_validez})"
- **Acción sugerida:** Contactar cliente o actualizar cotización antes de vencimiento

### 2. Nuevos Paquetes Activados

- **Trigger:** Paquete con activo=true creado en últimas 24 horas
- **Destinatarios:** Todos los usuarios del sistema
- **Mensaje:** "El paquete '{nombre}' para {destino} está ahora disponible"
- **Acción sugerida:** Revisar nuevo paquete para ofrecer a clientes

### 3. Nuevas Actividades Activadas

- **Trigger:** Actividad con activo=true creada en últimas 24 horas
- **Destinatarios:** Todos los usuarios del sistema
- **Mensaje:** "La actividad '{nombre}' de tipo {tipo} está ahora disponible"
- **Acción sugerida:** Revisar nueva actividad para incluir en cotizaciones

### 4. Cotización Confirmada - Inicio Próximo

- **Trigger:** Cotización en estado "confirmado" a 1 día de su fecha_inicio
- **Destinatario:** Usuario creador de la cotización
- **Mensaje:** "La cotización {codigo} inicia mañana ({fecha_inicio})"
- **Acción sugerida:** Confirmación final con cliente y proveedores

### 5. Seguimiento Post-Viaje

- **Trigger:** Cotización en estado "confirmado" 10 días después de su fecha_fin
- **Destinatario:** Usuario creador de la cotización
- **Mensaje:** "Han pasado 10 días desde el fin de la cotización {codigo}. Considera hacer seguimiento con el cliente."
- **Acción sugerida:** Contactar cliente para feedback, testimoniales o futuras reservas

---

## Configuración de Ejecución

- Frecuencia recomendada: Cada hora mediante cronjob o scheduler
- Función: `procesarNotificaciones`
- La función evita duplicados verificando notificaciones existentes
- Retorna estadísticas: número de notificaciones creadas
- No requiere autenticación (usa asServiceRole)

> **Estado actual:** La función `procesarNotificaciones` ya cuenta con una automatización programada activa, por lo que la generación de avisos se ejecuta de forma recurrente sin intervención manual.
