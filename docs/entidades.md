# Estructura de Datos

## Entidades Principales

`Cotizacion` · `Voucher` · `Cliente` · `Proveedor` · `Paquete` · `Actividad` · `Aerolinea`

## Entidades de Configuración

`ConfiguracionGeneral` · `GrupoUsuario` · `MetaMensual` · `ConfiguracionNotificacion` · `TipoTransferencia` · `TipoServicioTransferencia` · `Aeropuerto` · `TipoCama` · `TipoVista` · `TipoDormitorio`

## Entidades de Soporte y Operación

`Destino` · `Inclusion` · `Condicion` · `MetodoPago` · `CanalCliente` · `AmenidadServicio` · `CategoriaAmenidad` · `CategoriaInclusion` · `CategoriaCondicion` · `EtiquetaProveedor` · `Indicativo` · `ArchivosProveedores` · `ElementoPapelera` · `Notificacion` · `Favorito` · `ClienteFavorito`

> **Nota de estructura:** La operación diaria se apoya en entidades transaccionales (cotizaciones, vouchers, clientes y productos), mientras que la configuración del negocio vive en catálogos reutilizables para mantener consistencia en formularios, PDFs, correos y filtros.
