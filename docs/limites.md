# Límites y Restricciones

## Formatos Estrictos

- **DNI:** Exactamente 13 dígitos con formato `####-####-#####`
- **RTN:** Exactamente 14 dígitos con formato `####-####-######`
- **Códigos de cotización:** `COT-XXX` (numérico secuencial, 3 dígitos)
- **Códigos de paquete:** `P-XXX` (numérico secuencial, 3 dígitos)
- **Códigos de actividad:** `A-XXX` (numérico secuencial, 3 dígitos)

## Monedas Soportadas

- USD (Dólares estadounidenses)
- L (Lempiras hondureños) — etiqueta visible para el código HNL
- Conversión automática según tasa configurada
- Tasa global configurable en ConfiguracionGeneral
- Tasa personalizada opcional por proveedor
- Tasa manual opcional por cotización

## Operaciones No Permitidas

- No se pueden modificar usuarios directamente en la entidad User (solo invitaciones)
- No se puede cambiar el código de una cotización una vez creada
- No se puede restaurar un elemento de papelera si excedió el período de retención y fue eliminado automáticamente
- No se puede crear cotización sin cliente seleccionado
- No se puede crear cotización sin al menos 1 paquete o 1 actividad
- Las acciones masivas solo están disponibles para usuarios Admin y grupo Supervisor
