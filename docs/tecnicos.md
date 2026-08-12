# Detalles Técnicos

## Stack Tecnológico

**Frontend:**

- React 18.2
- Tailwind CSS para estilos
- shadcn/ui como biblioteca de componentes
- React Query (@tanstack/react-query) para gestión de estado
- React Router DOM para navegación
- date-fns para manejo de fechas
- Lucide React para iconografía
- @hello-pangea/dnd para drag-and-drop
- framer-motion para animaciones
- react-quill para editor de texto enriquecido

**Backend:**

- Base44 SDK en frontend y funciones serverless
- Deno Deploy para funciones backend
- jsPDF v2.5.1 para generación de PDF
- Resend + RESEND_API_KEY para correos transaccionales
- Core.UploadFile y Core.SendEmail en flujos heredados/complementarios
- Autenticación, permisos y entidades integradas en Base44

---

## Arquitectura de Componentes

**Organización de Archivos:**

- `pages/` - Páginas principales del sistema
- `components/` - Componentes reutilizables organizados por dominio
- `components/cotizacion/` y `components/voucher/` - Flujos documentales
- `components/configuracion/` - Catálogos, tipos, diseño y parámetros operativos
- `components/common/` - utilidades compartidas (exportación, papelera, tablas, modales)
- `components/pdf/` - Plantillas de PDF y secciones imprimibles
- `entities/` - esquemas JSON de entidades
- `functions/` - funciones backend y tareas automáticas
- `Layout.jsx` - layout global con sidebar colapsable y tooltips

---

## Patrones de Diseño Implementados

**Optimistic Updates**
React Query invalida queries después de mutaciones para reflejar cambios inmediatamente sin recargar página.

**Componentización Modular**
Separación estricta de responsabilidades: secciones de cotización (ClienteInfo, PaquetesSection, ActividadesSection, etc.) como componentes independientes.

**Custom Hooks**
`usePapelera`: lógica reutilizable para mover elementos a papelera desde cualquier módulo.

**Lazy Loading**
Queries con enabled condicional y paginación en listados grandes (ej: paquetes con 20 por página).
