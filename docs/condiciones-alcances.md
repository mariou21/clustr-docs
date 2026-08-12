# Condiciones de Uso y Alcances

## Condiciones de Uso

- El sistema está diseñado para uso exclusivo de personal autorizado de Travel Diunsa
- Los usuarios deben ser invitados por un administrador; no existe registro público
- Cada usuario es responsable de mantener la confidencialidad de sus credenciales
- Los permisos se asignan mediante grupos y roles; el administrador controla el acceso a módulos sensibles
- Las cotizaciones generadas son propiedad de la empresa y no deben compartirse fuera de canales autorizados
- Los enlaces públicos deben usarse con precaución y desactivarse cuando la cotización ya no esté vigente
- La información de clientes debe manejarse según políticas de privacidad y protección de datos
- Los precios y tasas de cambio deben actualizarse regularmente para reflejar condiciones de mercado

---

## Alcances Funcionales

### El Sistema PUEDE:

- Crear, editar, duplicar y eliminar cotizaciones con control de versiones completo
- Gestionar catálogos de paquetes, actividades, proveedores, destinos e inclusiones
- Configurar precios dinámicos por tipo de pasajero con rangos de edad personalizables
- Cotizar habitaciones por estadía completa o por noche en paquetes y alojamientos
- Aplicar tarifas especiales manuales por habitación con descripción promocional visible en documentos, mensajes y registros
- Generar PDFs profesionales con plantillas personalizables
- Compartir cotizaciones mediante enlaces públicos seguros
- Enviar cotizaciones por correo electrónico con diseño HTML personalizado
- Gestionar múltiples monedas con tasas de cambio automáticas
- Aplicar descuentos por paquete y globales para actividades
- Mantener historial completo de versiones de cotizaciones
- Rastrear estado de cotizaciones y actualizar automáticamente las vencidas
- Gestionar base de datos de clientes con sistema de favoritos por agente
- Configurar permisos granulares por grupo de usuario
- Recuperar elementos eliminados dentro del período de retención
- Exportar datos a CSV/Excel con filtros aplicados
- Reordenar elementos mediante drag-and-drop (categorías, inclusiones, condiciones, etc.)
- Gestionar múltiples oficinas con información de contacto independiente
- Centralizar parámetros de diseño (tipografías, colores botones, estilos tabla, paleta sidebar)
- Editar visualmente todos los parámetros de diseño sin tocar código

### El Sistema NO PUEDE:

- Procesar pagos directamente (requiere integración externa adicional)
- Generar reportes analíticos avanzados (solo exportación de datos)
- Sincronizar automáticamente con sistemas contables externos
- Gestionar inventarios en tiempo real de proveedores
- Enviar notificaciones automáticas push o SMS (solo correo electrónico)
- Crear usuarios sin intervención del administrador (no hay auto-registro)
- Recuperar elementos después de eliminación permanente o limpieza automática
- Manejar reservas confirmadas con gestión de calendario completa
- Integrar directamente con pasarelas de pago

---

## Consideraciones de Rendimiento

**Optimizaciones Implementadas:**

- Queries con `staleTime` para reducir refetching innecesario
- Paginación en lista de paquetes (20 por página)
- Lazy loading de datos de cliente solo cuando se selecciona
- Memoización de componentes sidebar para evitar re-renders
- Carga condicional de queries según parámetros URL
- Validación de imágenes antes de subida (tamaño y tipo)
