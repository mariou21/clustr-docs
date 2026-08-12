# Funcionalidades

## Metas Mensuales

El sistema incluye un módulo de seguimiento de metas mensuales para agentes de viajes, permitiendo establecer objetivos de ventas y monitorear su cumplimiento en tiempo real mediante gráficos visuales intuitivos.

**¿Qué mide?**

- **Cotizaciones Confirmadas:** Suma del valor total de todas las cotizaciones en estado "confirmado" creadas por el usuario en el mes actual
- **Cotizaciones Pendientes:** Suma del valor total de cotizaciones en estado "pendiente" del mes actual
- **Cotizaciones Vencidas:** Suma de cotizaciones que pasaron a estado "vencido" en el mes actual
- **Moneda:** Las metas pueden configurarse en USD o HNL

**Cómo funciona:**

1. **Establecer Meta:** En la página "Metas Mensuales" los administradores asignan un valor objetivo a cada agente para el mes actual
2. **Seguimiento Automático:** El sistema suma automáticamente todas las cotizaciones confirmadas del usuario en el mes
3. **Cálculo de Progreso:** Se calcula el porcentaje de cumplimiento dividiendo valor actual / meta × 100
4. **Actualización en Tiempo Real:** Las tarjetas del dashboard se actualizan automáticamente cada vez que se confirma o modifica una cotización

**Visualización en Dashboard:**

- **Card de Metas (Inicio):** Tres gráficos circulares (Gauge) mostrando Confirmadas, Pendientes y Vencidas
- Cada gráfico muestra porcentaje de cumplimiento (0-100%+)
- Colores: Verde (confirmadas), Naranja (pendientes), Rojo (vencidas)
- Información debajo: Meta en moneda, valor actual, faltante si no cumple
- Icono ↑ cuando meta está cumplida (≥100%)
- Mensaje "¡Meta cumplida!" en verde cuando llega a 100%

**Indicadores:**

- **0-99%:** Muestra falta restante (L. XXX.XX o $XXX.XX)
- **100%+:** Meta cumplida con ícono de tendencia hacia arriba
- El gráfico rellena el círculo proporcionalmente hasta 100%

**Tipos de Visualización:**

- **Horizontal:** Gráfico a la derecha, información a la izquierda (dashboard principal)
- **Vertical:** Gráfico arriba, información debajo (card individual)
- Tamaños: small (60px), medium (100px), large (120px)

**Datos Almacenados (Entidad MetaMensual):**

- `user_id`: ID del usuario asignado
- `mes`: Mes (1-12)
- `año`: Año de la meta
- `meta_valor`: Cantidad en dinero a alcanzar
- `moneda`: USD o HNL

---

## Gestión de Aerolíneas

Las aerolíneas son la base del módulo de vuelos. Se configura cada aerolínea disponible con sus características y tipos de tarifas.

**Información de Aerolínea:**

- **Nombre:** Nombre completo de la aerolínea (obligatorio)
- **Tipo:** Categoría de la aerolínea (Low-Cost, Full Service, etc.)
- **Código IATA:** Código de 2 letras (ej: AA, UA, DL)
- **Prefijo de Vuelo:** Identificador de vuelos (ej: AA100)
- **ID Alfa:** Identificador alfanumérico personalizado
- **País de Origen:** País donde opera la aerolínea
- **Logo:** Imagen de la aerolínea (PNG/JPG, máx. 2MB)
- **Activo:** Controla si la aerolínea está disponible en cotizaciones

**Tipos de Tarifa por Aerolínea:**

Cada aerolínea puede tener múltiples tipos de tarifa con características propias:

- **Nombre:** Ej: Económica, Business, Primera Clase
- **Inclusiones:** Servicios incluidos (equipaje, comidas, etc.)
- **Condiciones:** Políticas de cancelación, cambios, etc.

Los tipos de tarifa se seleccionan al crear itinerarios de vuelo.

---

## Itinerarios de Vuelo (Vuelos)

Los itinerarios son configuraciones pre-guardadas de rutas de vuelo que se pueden reutilizar en múltiples cotizaciones.

**Estructura de Itinerario:**

- **Nombre:** Descripción del itinerario (ej: "Vuelo a Miami por Panamá")
- **Código:** Identificador único auto-generado (ej: SPS-MIA-1)
- **Opciones:** Se puede definir una opción de vuelo con múltiples trayectos
- **Trayectos:** Cada trayecto representa un vuelo individual en la ruta

**Datos por Trayecto:**

- **Origen y Destino:** Códigos de aeropuerto (ej: SPS, MIA)
- **Aerolínea:** Selección de aerolínea registrada
- **Número de Vuelo:** Identificador del vuelo (ej: AA100)
- **Tipo de Tarifa:** Tarifa de la aerolínea seleccionada
- **Escala/Conexión:** Indicar si hay parada y tiempo de conexión (horas/minutos)

**Validaciones del Sistema:**

- Nombre del itinerario es obligatorio
- Cada trayecto debe tener origen, destino, aerolínea, número y tipo de tarifa
- Si hay conexión, el tiempo debe ser especificado (horas y/o minutos)
- Generación automática de código basado en ruta (origen-destino-secuencial)

---

## Integración de Vuelos en Cotizaciones

Los itinerarios de vuelo creados pueden ser agregados a una cotización de viaje.

**Flujo de Uso:**

1. **Desde Página Vuelos:**
   - Busca y filtra itinerarios por aerolínea, origen, destino o conexiones
   - Haz clic en el botón "Cotizar" en un itinerario
   - Se abre automáticamente una nueva cotización con el vuelo pre-cargado
2. **Desde Nueva Cotización:**
   - En la sección de Vuelos, busca y selecciona un itinerario guardado
   - Los datos de trayectos se cargan automáticamente
   - Puedes agregar precios manuales si no están precargados

**Precios en Cotización:**

- **Ingresar Valores Manuales:** Opción para definir precios por tipo de pasajero (adulto, niño, tercera edad y cuarta edad)
- **Tarifas especiales (3ra/4ta edad):** Toggles independientes que activan el modo tarifa especial para adultos mayores, replicando la lógica de exclusividad ya usada en paquetes y alojamientos
- **Descuentos:** Aplicables a nivel de vuelo (porcentual o fijo)
- **Moneda:** Los precios se visualizan en USD/HNL según configuración
- **Tasa de Cambio:** Se aplica automáticamente en conversiones

**Servicios Adicionales:**

- **Cuidado de Menores:** Servicio de acompañamiento
- **Asistencia Especial:** Pasajeros con movilidad reducida
- **Artículos Deportivos:** Equipamiento de deportes extremos
- **Mascotas:** Transporte de animales domésticos

---

## Acciones en Página Vuelos

**Operaciones Disponibles:**

- **Crear:** Nuevo itinerario con formulario completo
- **Editar:** Modificar itinerario existente
- **Duplicar:** Copiar un itinerario para crear variantes
- **Eliminar:** Remover un itinerario (requiere confirmación)
- **Cotizar:** Abrir nueva cotización con el itinerario pre-cargado

**Búsqueda y Filtros:**

- **Búsqueda:** Por nombre, código o aeropuerto
- **Filtro Aerolínea:** Ver solo itinerarios de una aerolínea
- **Filtro Origen:** Aeropuerto de salida
- **Filtro Destino:** Aeropuerto final
- **Filtro Conexiones:** Directo, 1 conexión, 2+ conexiones

**Permisos de Acceso:**

- **Ver:** Listar y buscar itinerarios (todos)
- **Crear:** Nuevos itinerarios (admin + permisos del grupo)
- **Editar:** Modificar itinerarios (admin + permisos del grupo)
- **Eliminar:** Remover itinerarios (admin + permisos del grupo)
