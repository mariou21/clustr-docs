# Guías de Administración

## Gestión de Usuarios y Permisos

**Roles Predefinidos:**

- **Admin:** Acceso completo a todo el sistema, incluida configuración y gestión de usuarios
- **User:** Acceso según permisos asignados por grupo

**Grupos Personalizados:**

Los grupos permiten asignar permisos granulares por módulo:

- Cotizaciones: ver, crear, editar, eliminar
- Paquetes: ver, crear, editar, eliminar
- Actividades: ver, crear, editar, eliminar
- Proveedores: ver, crear, editar, eliminar
- Clientes: ver, crear, editar, eliminar, ver_creador (solo cotizaciones propias)
- Usuarios: ver, crear, editar, eliminar
- Configuración: ver, editar

**Control Granular de Modal de Selección de Clientes:**

Permisos específicos para el modal de selección al cotizar:

- **Ver modal seleccionar cliente:** Controla si el grupo puede ver el botón y modal de selección
- **Campos visibles en el modal:** Define qué información del cliente se muestra en la lista
  - DNI/RTN - Mostrar identificador fiscal
  - Correo - Mostrar correo electrónico
  - Teléfono - Mostrar número de teléfono
  - Ciudad - Mostrar ubicación del cliente
- **Campos permitidos para búsqueda:** Restringe por qué campos se puede buscar
  - Nombre, Apellido, Correo, Teléfono

> El placeholder del campo de búsqueda se actualiza dinámicamente mostrando solo los campos permitidos. Si todos los campos de búsqueda están deshabilitados, el campo de búsqueda se deshabilita automáticamente.

**Procedimiento para Crear Grupo:**

1. Ir a Configuración → Usuarios → pestaña "Grupos"
2. Clic en "Nuevo Grupo"
3. Asignar nombre descriptivo y color identificador
4. Definir permisos por cada módulo mediante switches
5. Guardar grupo
6. Asignar usuarios al grupo desde la lista de usuarios

**Perfiles de Usuario Extendidos:**

Los usuarios pueden tener campos adicionales para aparecer en PDFs y correos:

- Cargo (ej: "Agente de Viajes Senior")
- Oficina (ej: "Tegucigalpa Centro")
- Teléfono de Trabajo
- Foto de Perfil

---

## Configuración General del Sistema

**Parámetros Críticos:**

| Parámetro | Valor |
|---|---|
| Tasa de Cambio USD→L | Configurable (default: 30.00) |
| Moneda Predeterminada | USD o L |
| Zona Horaria | America/Tegucigalpa (default) |
| Formato de Fecha | DD/MM/YYYY, MM/DD/YYYY, YYYY-MM-DD |
| Idioma | Español (es) o Inglés (en) |
| Días Retención Papelera | 180 días (configurable) |
| Hora Limpieza Papelera | 00:00 hrs (configurable) |

**Configuración de Oficinas Múltiples:**

Cada oficina puede tener: nombre, dirección específica, teléfono, ciudad y estado activa/inactiva.

---

## Mantenimiento y Tareas Administrativas

**Tareas Automáticas Configuradas:**

- **Verificación de Cotizaciones Vencidas:** Se ejecuta también desde el frontend al cargar Inicio y Cotizaciones. Actualiza automáticamente cotizaciones pendientes con fecha_validez expirada al estado "vencido".
- **Limpieza de Papelera:** Cronjob programado para ejecutarse a la hora configurada (default: 00:00). Elimina permanentemente elementos que excedan dias_retencion_papelera.
- **Procesamiento de Notificaciones:** Función procesarNotificaciones ejecutable periódicamente (recomendado: cada hora). Genera notificaciones automáticas.

**Tareas Manuales Recomendadas:**

- Revisión mensual de catálogo de paquetes y actividades (actualizar precios, desactivar obsoletos)
- Actualización trimestral de tasa de cambio según mercado
- Auditoría de proveedores activos y actualización de contactos
- Revisión de clientes inactivos para depuración de base de datos
- Backup periódico de configuraciones personalizadas (plantillas, condiciones estándar)
- Revisión de papelera antes de vaciado automático
- Exportación mensual de cotizaciones confirmadas para reportes

**Exportación de Datos:**

Todos los módulos principales incluyen botones de exportación:

- Formato CSV para análisis en Excel/Google Sheets
- Formato Excel (XML) para compatibilidad directa con Microsoft Office
- Respeta los filtros aplicados en la vista actual
- Incluye todos los campos relevantes configurados por columnas
