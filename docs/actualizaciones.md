# Información del Sistema

## Versión y Entorno

- **Versión del Sistema:** Ver badge en la parte superior de la documentación
- **Plataforma Base44:** V3+
- **Entorno:** Producción

---

## Cambios Relevantes Documentados

### Voucher y traslados

- Gestión de vouchers con flujo por cotización, producto o creación manual
- Soporte para paquete, alojamiento, actividad y traslado
- Nuevas entidades TipoTransferencia y TipoServicioTransferencia
- Configuración de traslados dentro de Configuración → Tipos

### Diseño centralizado

- Parámetros de diseño globales en ConfiguracionGeneral
- Paleta de botones, sidebar, tipografías y tablas estándar
- Estilo destacado global para Tipos de Paquete y Tipos de Actividad, aplicado por registro cuando una etiqueta se marca como destacada
- Documentos y vistas sincronizados con configuración visual

### Dashboard y navegación

- Página principal consolidada como Panel Principal
- Tarjetas resumen de vouchers más compactas y legibles
- Tooltips de sidebar optimizados en modo colapsado

### Cotización por pasos

- Nueva Cotización ahora usa un menú lateral por pasos para reducir el scroll continuo
- Los paneles principales se muestran uno a la vez manteniendo los mismos componentes y la misma información operativa
- Las opciones de vuelos pueden navegarse como subitems del menú lateral, sin tabs dentro del panel
- Habitaciones de paquetes y hoteles ahora admiten tarifa especial manual con descripción promocional y persistencia en cotización, PDF, vista pública, correo y mensajería
- Las habitaciones de paquetes y alojamientos ahora pueden cotizarse por estadía o por noche, recalculando automáticamente según el rango de fechas seleccionado
- Al seleccionar Tipos Precargados activos, la ocupación y sus cantidades predeterminadas se respetan tanto en tarifa por estadía como en tarifa por noche
- El bloque de paquetes en cotización se rediseñó para verse más limpio: menos cajas anidadas, resumen superior y habitaciones plegables más compactas
- Las condiciones específicas de cada paquete ahora se persisten dentro de la cotización (paquete_condiciones) y se recuperan automáticamente del paquete original al editar una cotización previa que no las tuviera guardadas
- El drawer de Ver Cotización muestra las condiciones específicas por paquete en un bloque dedicado
- Las plantillas PDF (Minimalista y Beta) renderizan las condiciones específicas de cada paquete dentro de su tarjeta
- La conversión de moneda respeta la tasa específica del proveedor de cada paquete y actividad (origen_tasa = proveedor) en lugar de aplicar la tasa global
- El Resumen incluye un selector por producto para activar o desactivar la tasa específica del proveedor
- Tarifas especiales de 3ra y 4ta edad en habitaciones: cada habitación incorpora un toggle para activar precios especiales, replicando el modelo de Vuelos
- Regla de exclusividad de descuentos: al activar la tarifa especial de 3ra edad en cualquier habitación, el descuento global de 3ra edad del Resumen se bloquea y desactiva automáticamente (y viceversa para 4ta edad)
- Las tarifas especiales de 3ra y 4ta edad se muestran como filas adicionales en el Ver Cotización, PDF y mensajería

### Documentos PDF y mensajería

- La sección Plantillas ahora separa la configuración PDF de descarga y correo para cotizaciones
- Cada salida puede definir su propia plantilla, secciones visibles, márgenes y estilos de forma independiente
- El desglose de habitaciones en PDF y mensaje ahora muestra el Tipo de Precio (Estadía o Pasajero/Noche) como etiqueta ámbar junto al subtotal
- La tabla de pasajeros en el PDF incluye una columna Precio Unit. con el precio aplicado por cada tipo de pasajero
- Corrección: al editar una cotización y guardar una nueva versión, el PDF y el mensaje ahora reflejan los cambios inmediatamente
- El desglose de vuelos en PDF ahora incluye una tabla con cantidad, precio unitario y subtotal por tipo de pasajero
- Doble moneda en cotizaciones: un interruptor en el Resumen activa la visualización simultánea de USD y L (HNL) en columnas paralelas

### Integridad de datos — Aeropuertos

- Nuevo campo `zona_horaria` en la entidad Aeropuerto (formato IANA) para el cálculo correcto de la duración de vuelos considerando DST
- Selector desplegable TimezoneSelect en Configuración → Destinos → Aeropuertos: lista canónica IANA tomada del navegador
- Validación en línea: la zona seleccionada se comprueba con Intl.DateTimeFormat antes de guardar; valores legacy inválidos se marcan en rojo

### Automatizaciones y soporte operativo

- Programación activa para verificación de cotizaciones vencidas
- Programación activa para notificaciones automáticas
- Automatizaciones de borrado en cascada para catálogos maestros

---

## Estructura Escalable

- Arquitectura modular por dominio funcional
- Entidades extensibles para nuevos productos y documentos
- Plantillas reutilizables para PDF, correo y vista pública
- Funciones backend independientes y automatizables

> **Estado actual:** La documentación quedó alineada con la versión operativa actual del sistema, incluyendo vouchers, traslados, automatizaciones, estructura de entidades, stack real y configuración visual vigente.
