### Descripción:

Recursos auxiliares para preparar el alta de ventas por API v2.

### Autenticación:

Todos los endpoints de esta guía utilizan el mismo `access_token` del resto de la API v2.

### Endpoints disponibles:

|Endpoint|Uso|
|---|---|
|`GET /api/v2/ventas/puntos_venta`|Consulta talonarios habilitados para ventas|
|`GET /api/v2/ventas/puntos_venta_cobro`|Consulta talonarios habilitados para cobros/recibos|
|`GET /api/v2/ventas/formas_entrega`|Consulta remitos/formas de entrega y opciones especiales (`pendiente`, `no_stock`)|
|`GET /api/v2/ventas/domicilios_entrega?id_cliente=...`|Consulta domicilios de entrega del cliente|
|`GET /api/v2/ventas/empresas_transporte`|Consulta transportistas|
|`GET /api/v2/ventas/tarjetas`|Consulta tarjetas habilitadas|
|`GET /api/v2/ventas/entidades`|Consulta entidades emisoras/bancarias|
|`GET /api/v2/ventas/planes_tarjeta?id_tarjeta=...&id_entidad=...`|Consulta planes vigentes para una tarjeta y entidad|
|`GET /api/v2/ventas/cuotas_plan?id_plan=...`|Consulta cuotas configuradas para un plan|
|`GET /api/v2/ventas/cuentas_bancarias`|Consulta cuentas bancarias para los movimientos bancarios de `contado_mixto`|
|`GET /api/v2/ventas/tipos_retencion`|Consulta tipos de retención habilitados para `contado_mixto`|
|`GET /api/v2/impuestos/tipos_percepcion`|Consulta tipos de percepción disponibles|
|`GET /api/v2/impuestos/regimenes`|Consulta regímenes impositivos|

### Ejemplos:

#### Puntos de venta
```bash
curl 'https://cianbox.org/micuenta/api/v2/ventas/puntos_venta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_cliente=257'
```

#### Puntos de venta de cobro
```bash
curl 'https://cianbox.org/micuenta/api/v2/ventas/puntos_venta_cobro?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_punto_venta_venta=1'
```

#### Tarjetas
```bash
curl 'https://cianbox.org/micuenta/api/v2/ventas/tarjetas?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

#### Planes de tarjeta
```bash
curl 'https://cianbox.org/micuenta/api/v2/ventas/planes_tarjeta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_tarjeta=32&id_entidad=1'
```

#### Cuotas de un plan
```bash
curl 'https://cianbox.org/micuenta/api/v2/ventas/cuotas_plan?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_plan=1'
```

#### Cuentas bancarias
```bash
curl 'https://cianbox.org/micuenta/api/v2/ventas/cuentas_bancarias?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

#### Tipos de retención
```bash
curl 'https://cianbox.org/micuenta/api/v2/ventas/tipos_retencion?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

#### Tipos de percepción
```bash
curl 'https://cianbox.org/micuenta/api/v2/impuestos/tipos_percepcion?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Notas:

- Los listados siguen el esquema estándar de paginación de API v2 (`page`, `limit`, `total_pages`).
- `planes_tarjeta` y `cuotas_plan` pueden devolver un `body` vacío si la cuenta todavía no configuró planes.
- Para `contado_mixto`, el `id_punto_venta` del bloque `cobro` debe salir de un talonario de cobros/recibos, no de uno de ventas.
- `puntos_venta_cobro?id_punto_venta_venta=...` ayuda a encontrar sólo talonarios de cobro con la misma fiscalidad que la venta.
- `formas_entrega` ya incluye los talonarios reales de remito y también las opciones especiales `0` (remito interno), `pendiente` y `no_stock`.
- `cuentas_bancarias` se usa para `depositos[]`, que cubre tanto depósitos como transferencias bancarias.
- No existe un array separado `transferencias[]` en el contrato público de `ventas/alta`; todos los movimientos bancarios van por `depositos[]`.
- `tipos_retencion` se usa para completar `retenciones[]`.
- Para `valores[]`, la entidad bancaria sale de `GET /api/v2/ventas/entidades`; no hay un recurso separado de "tipos de valor" porque el contrato de alta replica los campos que consume el recibo del sistema.
