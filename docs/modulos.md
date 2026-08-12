# Módulos del Sistema

## Módulo de Cotizaciones

Núcleo del sistema que permite crear, editar y gestionar propuestas de viaje completas.

**Características:**

- Creación de cotizaciones con códigos únicos (COT-001, COT-002, etc.)
- Selección de cliente y gestión de información del destinatario
- Agregado de hasta 3 paquetes por cotización
- Agregado de hasta 7 actividades adicionales por cotización
- Configuración de fechas de viaje y validez de la cotización
- Gestión de estados: Borrador, Pendiente, Confirmado, Vencido
- Versionado automático al editar (v.1, v.1.1, v.1.2, etc.)
- Historial de versiones con totales y fechas
- Cálculo automático de totales con descuentos aplicables
- Soporte para múltiples monedas (USD/HNL) con conversión automática
- Descuentos por paquete y descuento global para actividades
- Selección de condiciones y métodos de pago
- Vista previa rápida de cotizaciones
- Compartir mediante enlace público personalizado
- Envío por correo electrónico con plantillas personalizables
- Exportación a PDF con diseños profesionales

## Módulo de Vouchers

Emisión y gestión de vouchers operativos para servicios confirmados, con enfoque documental y trazabilidad por versión.

**Características:**

- Códigos únicos tipo V-001, V-002, etc.
- Estados de voucher: borrador, emitido y anulado
- Tres flujos de creación: desde cotización, desde producto o manual
- Tipos de servicio: Paquete, Alojamiento, Actividad y Traslado
- Historial de versiones por voucher
- Datos de cliente, proveedor, localizador y agente integrados
- Habitaciones, inclusiones, amenidades y condiciones generales editables
- PDF descargable y envío por correo de voucher
- Vista rápida y acciones de duplicado / edición
- Soporte inicial para vouchers de traslado con pasajeros, aeropuertos y vuelos

## Módulo de Paquetes

Catálogo de paquetes turísticos con información detallada, precios base e inclusiones.

**Características:**

- Código único autogenerado (P-001, P-002, etc.)
- Soporte para múltiples destinos por paquete
- Asociación con proveedor específico
- Inclusiones personalizables con iconos
- Políticas de cancelación específicas
- Imágenes de alta calidad (máx. 2MB, formato 1200×800px recomendado)
- Precios base por tipo de pasajero (Adulto, Junior, Niño, Infante)
- Tipos de transporte (Ferry, Avión SPS/TGU, Terrestre, Otro)
- Estados activo/inactivo
- Vista en cuadrícula o lista
- Duplicación de paquetes existentes
- Botón directo "Cotizar" desde la tarjeta del paquete
- Filtros por destino, proveedor, transporte y estado
- Ordenamiento múltiple (fecha, nombre, etc.)

## Módulo de Actividades

Gestión de actividades y experiencias adicionales con precios dinámicos por producto.

**Características:**

- Código único autogenerado (A-001, A-002, etc.)
- Tipos de actividad: Acuática, Aventura, Gastronómica, Cultural, Deportiva, Otra
- Sistema de productos múltiples por actividad
- Dos modelos de precio: por pasajero o por actividad completa
- Configuración de rangos de edad por tipo de pasajero
- Capacidad mínima y máxima por producto
- Descripción breve y detallada separadas
- Indicaciones especiales y punto de encuentro
- Soporte para múltiples destinos
- Inclusiones personalizables
- Asociación con proveedor
- Flag opcional "con_horario"
- Filtros por tipo, destino, proveedor y estado
- Botón directo "Cotizar" desde la tarjeta de actividad

## Módulo de Clientes

Base de datos completa de clientes con perfiles detallados y sistema de favoritos.

**Características:**

- Dos tipos de cliente: Directo (persona física) y Empresa
- DNI para clientes directos (formato ####-####-#####)
- RTN para empresas (formato ####-####-######)
- Datos de contacto: correo, teléfono, dirección completa
- Información de pasaporte y fecha de nacimiento
- Estado de Visa USA con fecha de vencimiento
- Canal de procedencia (WhatsApp, Instagram, etc.)
- Preferencia de suscripción informativa
- Notas internas privadas del agente
- Sistema de clientes favoritos por agente
- Búsqueda avanzada por nombre, correo, teléfono o identificador fiscal
- Vista detallada con historial de cotizaciones
- Copia rápida de datos al portapapeles
- Estados activo/inactivo
- Exportación a CSV/Excel

## Módulo de Proveedores

Directorio de proveedores de servicios turísticos con categorización y contactos.

**Características:**

- ID único personalizable por proveedor
- Categorías configurables (Hotel, Transporte, Tour Operador, etc.)
- Información de contacto completa (persona, teléfono, correo, dirección)
- Asignación de múltiples destinos operativos
- Logo/imagen del proveedor (máx. 1MB)
- Inclusiones y servicios ofrecidos
- Tasa de cambio personalizada por proveedor (opcional)
- Condiciones específicas del proveedor
- Notas internas
- Vista en cuadrícula o lista
- Filtros por tipo, destino y estado
- Categorías drag-and-drop reordenables
- Acciones masivas (activar, desactivar, eliminar)

## Módulo de Vuelos

Gestión de aerolíneas e itinerarios de vuelo reutilizables para incluir en cotizaciones.

**Características:**

- Registro de aerolíneas con código IATA, prefijo de vuelo, logo y país de origen
- Tipos de tarifa por aerolínea (Económica, Business, Primera Clase, etc.)
- Inclusiones y condiciones específicas por tipo de tarifa
- Creación de itinerarios reutilizables con estructura modular
- Soporte para múltiples trayectos con conexiones y escalas
- Configuración de tiempo de conexión (horas/minutos)
- Generación automática de códigos de itinerario (ORIG-DEST-SECUENCIAL)
- Búsqueda y filtrado por aerolínea, origen, destino y número de conexiones
- Precios manuales por tipo de pasajero (Adulto, Niño, Tercera Edad)
- Servicios adicionales (cuidado menores, asistencia especial, equipaje deportivo, mascotas)
- Descuentos aplicables a nivel de vuelo
- Botón "Cotizar" para abrir inmediatamente una cotización con el itinerario
- Acciones: crear, editar, duplicar, eliminar, usar en cotización
- Validación automática de campos obligatorios por trayecto

## Módulo de Configuración

Panel centralizado para configurar todos los aspectos operativos y visuales del sistema.

**Secciones:**

1. **General** - Empresa, contacto, moneda, zona horaria, papelera, oficinas y versión del sistema.
2. **Usuarios** - Gestión de usuarios y grupos con permisos granulares por módulo.
3. **Destinos** - Catálogo base de destinos.
4. **Inclusiones** - Biblioteca reutilizable para paquetes, actividades y aerolíneas.
5. **Servicios** - Amenidades y servicios complementarios con estilos configurables.
6. **Tipos** - Tipos de actividad, paquete, indicativos, habitaciones y traslados.
7. **Condiciones** - Términos reutilizables para cotizaciones y vouchers.
8. **Pagos** - Métodos de pago y estructura visible en documentos.
9. **Canales** - Canales de captación del cliente.
10. **Plantillas** - Correos, vista pública, mensajería y diseñador PDF.
11. **Documentación** - Portal técnico interno actualizado desde el sistema.
12. **Papelera** - Restauración o eliminación definitiva según retención configurada.
