# API Externa

## Endpoint: validarCotizacionPublica

**Propósito:** Validar y obtener datos completos de una cotización mediante su código de acceso público. Este endpoint está diseñado para ser consumido por la aplicación pública de consulta de cotizaciones.

**URL del Endpoint:**

```
POST https://cluster-traveldiunsa.base44.app/api/functions/validarCotizacionPublica
```

**Headers Requeridos:**

- `Content-Type: application/json`
- `x-api-key: [VALOR_DEL_SECRETO]` — 🔐 Valor configurado en el secreto `PUBLIC_APP_API_KEY_CLUSTER_TRAVELDIUNSA`

**Body del Request (JSON):**

```json
{
  "codigo_acceso": "21713OM3"
}
```

`codigo_acceso`: Código único de acceso de 8 caracteres alfanuméricos asignado a cada cotización.

---

## Posibles Respuestas

**✅ 200 OK - Cotización encontrada:**

```json
{
  "cotizacion": { /* Objeto Cotizacion completo */ },
  "cliente": { /* Objeto Cliente completo */ },
  "config": { /* Objeto ConfiguracionGeneral */ }
}
```

**❌ 401 Unauthorized - API Key inválida:**

```json
{ "error": "No autorizado: clave API inválida" }
```

**❌ 400 Bad Request - Falta codigo_acceso:**

```json
{ "error": "Se requiere el código de acceso" }
```

**❌ 404 Not Found - Cotización no existe:**

```json
{ "error": "Cotización no encontrada o código de acceso inválido" }
```

**❌ 500 Internal Server Error:**

```json
{ "error": "Mensaje descriptivo del error" }
```

---

## Schemas Completos de Respuesta

### 🟢 Schema: Cotizacion

```json
{
  "id": "string (UUID)",
  "created_date": "string (ISO 8601 datetime)",
  "updated_date": "string (ISO 8601 datetime)",
  "created_by": "string (email del creador)",

  "codigo": "string (ej: 'COT-001')",
  "version": "string (ej: 'v.1', 'v.1.1')",
  "codigo_acceso": "string (8 chars, ej: '21713OM3')",

  "historial_versiones": [
    {
      "version": "string",
      "total": "number",
      "moneda": "string ('USD' | 'HNL')",
      "fecha": "string (ISO 8601 datetime)"
    }
  ],

  "cliente_id": "string (UUID del cliente)",
  "fecha_cotizacion": "string (ISO date: YYYY-MM-DD)",
  "fecha_validez": "string | null (ISO date: YYYY-MM-DD)",

  "tipo_tasa_cambio": "string ('predeterminada' | 'manual')",
  "tasa_cambio_manual": "number | null",

  "paquetes": [ /* array, máximo 3 */ ],
  "pasajeros": { "adultos": "number", "juniors": "number", "ninos": "number", "infantes": "number" },
  "actividades": [ /* array, máximo 7 */ ],
  "condiciones": ["string"],
  "metodos_pago": [ { "metodo_id": "string", "nombre": "string", "tipo": "string" } ],

  "descuento_global": { "activo": "boolean", "tipo": "string", "valor": "number" },

  "subtotal_paquetes": "number",
  "subtotal_actividades": "number",
  "total_descuentos": "number",
  "total": "number",
  "moneda": "string ('USD' | 'HNL')",
  "estado": "string ('borrador' | 'pendiente' | 'confirmado' | 'vencido')",
  "mensaje_personalizado": "string | null"
}
```

### 🔵 Schema: Cliente

```json
{
  "id": "string (UUID)",
  "created_date": "string (ISO 8601 datetime)",
  "updated_date": "string (ISO 8601 datetime)",
  "created_by": "string (email)",

  "nombre": "string (nombre o razón social)",
  "apellido": "string | null (solo para tipo Directo)",
  "tipo_cliente": "string ('Directo' | 'Empresa')",
  "canal": "string (canal de procedencia)",

  "identificador_fiscal": "string (DNI o RTN)",
  "pasaporte": "string | null",

  "telefono": "string",
  "correo": "string (email)",
  "fecha_nacimiento": "string | null (ISO date)",

  "direccion": "string",
  "ciudad": "string",
  "pais": "string",

  "tiene_visa_usa": "boolean",
  "fecha_vencimiento_visa_usa": "string | null (ISO date)",

  "acepta_suscripcion_informativa": "boolean",
  "notas_internas": "string"
}
```

### 🟣 Schema: ConfiguracionGeneral

```json
{
  "id": "string (UUID)",
  "nombre_empresa": "string",
  "direccion": "string",
  "telefono": "string",
  "correo": "string (email)",
  "sitio_web": "string (URL)",
  "logo_url": "string (URL)",

  "oficinas": [ { "nombre": "string", "direccion": "string", "telefono": "string", "ciudad": "string", "activa": "boolean" } ],

  "tasa_cambio_usd_hnl": "number (default: 30.0)",
  "moneda_defecto": "string ('USD' | 'HNL')",
  "zona_horaria": "string (default: 'America/Tegucigalpa')",
  "formato_fecha": "string ('DD/MM/YYYY' | 'MM/DD/YYYY' | 'YYYY-MM-DD')",
  "idioma": "string ('es' | 'en')",

  "notificaciones_email": "boolean",
  "version_sistema": "string",
  "estado_version": "string ('alpha' | 'beta' | 'rc' | 'release')",
  "build_date": "string",

  "dias_retencion_papelera": "number (default: 180)",
  "hora_limpieza_papelera": "string (HH:MM, default: '00:00')",

  "plantilla_correo": { /* estilos y textos */ },
  "plantilla_vista_publica": { /* estilos y textos */ },
  "plantilla_mensajeria": { /* estilos y textos */ }
}
```

---

## Ejemplos de Implementación

### 📝 JavaScript (Fetch API)

```javascript
const codigoAcceso = "21713OM3";
const apiKey = "TU_API_KEY_AQUI";

try {
  const response = await fetch(
    "https://cluster-traveldiunsa.base44.app/api/functions/validarCotizacionPublica",
    {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "x-api-key": apiKey
      },
      body: JSON.stringify({ codigo_acceso: codigoAcceso })
    }
  );

  if (!response.ok) {
    const error = await response.json();
    throw new Error(error.error || "Error al validar cotización");
  }

  const { cotizacion, cliente, config } = await response.json();
  console.log("Cotización:", cotizacion.codigo, cotizacion.version);
  console.log("Cliente:", cliente.nombre, cliente.apellido);
  console.log("Total:", cotizacion.total, cotizacion.moneda);
} catch (error) {
  console.error("Error:", error.message);
}
```

### ⚛️ React + useState

```jsx
import { useState, useEffect } from 'react';

function VistaCotizacion({ codigoAcceso }) {
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [data, setData] = useState(null);

  useEffect(() => {
    async function cargarCotizacion() {
      try {
        const response = await fetch(
          "https://cluster-traveldiunsa.base44.app/api/functions/validarCotizacionPublica",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
              "x-api-key": process.env.REACT_APP_API_KEY
            },
            body: JSON.stringify({ codigo_acceso: codigoAcceso })
          }
        );
        if (!response.ok) throw new Error((await response.json()).error);
        setData(await response.json());
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }
    if (codigoAcceso) cargarCotizacion();
  }, [codigoAcceso]);

  if (loading) return <div>Cargando cotización...</div>;
  if (error) return <div>Error: {error}</div>;
  if (!data) return null;

  const { cotizacion, cliente, config } = data;
  return (
    <div>
      <h1>{cotizacion.codigo} ({cotizacion.version})</h1>
      <h2>Cliente: {cliente.nombre} {cliente.apellido}</h2>
      <p>Total: {cotizacion.total} {cotizacion.moneda}</p>
    </div>
  );
}
```

### 🔧 cURL (Testing desde terminal)

```bash
curl -X POST https://cluster-traveldiunsa.base44.app/api/functions/validarCotizacionPublica \
  -H "Content-Type: application/json" \
  -H "x-api-key: TU_API_KEY_AQUI" \
  -d '{"codigo_acceso":"21713OM3"}'
```

---

## Notas de Seguridad

- El API Key debe mantenerse **SECRETO** y nunca exponerse en el código del frontend
- Usar variables de entorno para almacenar el API Key
- En aplicaciones frontend, hacer las llamadas desde el backend o usar funciones serverless
- Implementar rate limiting si se expone públicamente
- Validar siempre que la respuesta sea exitosa antes de usar los datos
- El endpoint solo retorna cotizaciones con codigo_acceso válido

## Consideraciones de Integración

- Los datos retornados incluyen **TODA** la información necesaria para renderizar la cotización completa
- Los arrays pueden estar vacíos ([]) pero nunca null
- Los campos opcionales pueden ser null
- Las fechas están en formato ISO 8601
- Los UUIDs son strings en formato estándar
- La moneda siempre será 'USD' o 'HNL'
- Los totales son números decimales (pueden tener centavos)
- El campo `plantilla_vista_publica` en config contiene la configuración de visualización
