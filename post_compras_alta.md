### Descripción:

Crea una nueva compra reutilizando el circuito real de `modules/pv_compras/alta_proc.php`.

Cuando la forma de pago es `contado_mixto`, el endpoint completa el flujo creando e imputando una orden de pago con `modules/pv_caja/alta_orden_pago_proc.php`.

### URL:

`https://cianbox.org/{cuenta}/api/v2/compras/alta`

### Método: POST

### Payload base:

```json
{
    "fecha_comprobante": "2026-06-29",
    "fecha_contabilizacion": "2026-06-29",
    "id_proveedor": 12,
    "forma_pago": "cuenta_corriente",
    "id_comprobante": 1,
    "id_tipo": 1,
    "punto_venta": 1,
    "numero": 12345,
    "id_contribuyente": 0,
    "id_moneda": 1,
    "cotizacion": 1,
    "observaciones": "Compra generada por integracion API",
    "recibida": "toda_sr",
    "productos": [
        {
            "tipo": "producto",
            "id": 95,
            "cantidad": 1,
            "neto_uni": 1000,
            "alicuota": 21
        }
    ],
    "percepciones": []
}
```

### Formas de pago soportadas:

|`forma_pago`|`id_forma_pago`|Descripción|
|---|---:|---|
|`cuenta_corriente`|`1`|Genera la compra en cuenta corriente del proveedor|
|`ctacte`|`1`|Alias de `cuenta_corriente`|
|`contado_mixto`|`2`|Genera la compra en cuenta corriente y luego crea una orden de pago imputada a esa compra|
|`contado`|`3`|Genera la compra de contado usando la caja del usuario de la API|
|`efectivo`|`3`|Alias de `contado`|

Debe informarse `forma_pago` o `id_forma_pago`. El endpoint no aplica una forma de pago predeterminada. Si se envían ambos campos, se usa `id_forma_pago`.

### Recursos auxiliares:

- `GET /api/v2/proveedores` permite obtener `id_proveedor` y defaults del proveedor.
- `GET /api/v2/proveedores/alta` devuelve el ejemplo para cargar proveedores por API.
- `GET /api/v2/compras/comprobantes` permite obtener `id_comprobante`.
- `GET /api/v2/compras/tipos` permite obtener `id_tipo`.
- `GET /api/v2/compras/contribuyentes` permite obtener `id_contribuyente` o resolverlo por CUIT.
- `GET /api/v2/compras/puntos_ventas_pago` permite obtener `pago.id_punto_venta` para `contado_mixto`.
- `GET /api/v2/compras/gastos` permite obtener IDs de `tabla_gastos` para ítems `tipo = gasto`.
- `GET /api/v2/compras/bienes_uso` permite obtener IDs de `tabla_bienes_uso` para ítems `tipo = bien_uso`.
- `GET /api/v2/impuestos/tipos_percepcion?vigente=true` permite obtener `percepciones[].id_percepcion` y su `id_impuesto`.
- `GET /api/v2/impuestos/regimenes?id_tipo_percepcion=...&vigente=true` permite obtener `percepciones[].id_regimen`.
- `GET /api/v2/caja/cuentas_bancarias` permite obtener `pago.transferencias[].id_cuenta`.
- `GET /api/v2/caja/transferencias_pendientes` permite obtener `pago.transferencias_pendientes[].id_transferencia`.
- `GET /api/v2/caja/valores` permite obtener `pago.valores[].id_valor`.
- `GET /api/v2/caja/chequeras` y `POST /api/v2/caja/valores/alta` permiten emitir cheques propios y usar el `id_valor` resultante.
- `GET /api/v2/caja/tipos_retencion` permite obtener `pago.retenciones[].id_retencion`, `punto_venta` y `numero` sugerido.
- `GET /api/v2/impuestos/regimenes?id_tipo_retencion=...` permite obtener `pago.retenciones[].id_regimen`.
- `GET /api/v2/impuestos/sujetos_suspendidos` permite obtener `pago.retenciones[].id_ss`.

### Campos principales:

|Campo|Requerido|Descripción|
|---|---|---|
|fecha_comprobante|SI|Fecha del comprobante, formato `YYYY-MM-DD`|
|fecha_contabilizacion|NO|Fecha contable. Si se omite usa `fecha_comprobante`|
|fecha_vencimiento|NO|Si se omite se calcula con el plazo del proveedor|
|id_proveedor|SI|Proveedor vigente|
|forma_pago|SI|`cuenta_corriente`, `contado_mixto`, `contado` o `efectivo`. También puede enviarse `id_forma_pago`|
|id_comprobante|SI|Comprobante vigente y habilitado, obtenido desde `GET /api/v2/compras/comprobantes`|
|id_tipo|SI|Tipo/letra vigente y habilitado, obtenido desde `GET /api/v2/compras/tipos`|
|punto_venta|SI|Punto de venta del comprobante de compra|
|numero|SI|Número del comprobante de compra|
|id_contribuyente|NO|Contribuyente fiscal de la compra. `0` representa el contribuyente principal|
|cuit_contribuyente|NO|Alternativa para resolver el contribuyente por CUIT cuando no se informa `id_contribuyente`|
|id_moneda|NO|Si se omite usa la moneda principal|
|cotizacion|NO|Si se omite usa la cotización vigente de la moneda|
|observaciones|NO|Texto libre|
|recibida|NO|`toda_sr`, `otras` o `no_stock`. Predeterminado: `toda_sr`|

Si la cuenta tiene multicontribuyente activo y no se informa `id_contribuyente` ni `cuit_contribuyente`, se usa el contribuyente predeterminado de compras configurado en la cuenta.

### Ítems:

`productos[]` acepta ítems de tipo `producto`, `gasto`, `bien_uso` y `concepto`. El nombre del array se mantiene por compatibilidad con el circuito legacy, pero no está limitado a productos de stock.

|Tipo|Tabla/uso|ID permitido|
|---|---|---|
|`producto`|`tabla_productos`|Obligatorio|
|`gasto`|`tabla_gastos`|Opcional. Si falta, se crea o reutiliza por `detalle`|
|`bien_uso`|`tabla_bienes_uso`|Opcional. Si falta, se crea o reutiliza por `detalle` + `id_tipo_bien_uso`|
|`concepto`|Concepto libre de compra|No usa ID|

```json
{
    "tipo": "producto",
    "id": 95,
    "detalle": "Producto de prueba",
    "cantidad": 1,
    "neto_uni": 1000,
    "alicuota": 21,
    "id_cuenta": 0,
    "descuento": 0,
    "imp_interno": 0
}
```

Reglas:

- `cantidad`, `neto_uni` y `alicuota` son obligatorios por ítem.
- Para `producto`, `id` debe existir y estar vigente.
- Para `gasto`, `id` es opcional. Si se informa, debe existir en `tabla_gastos`. Si se omite, `detalle` es obligatorio y el sistema puede crear o reutilizar el gasto por descripción.
- Para `bien_uso`, `id` es opcional. Si se informa, debe existir en `tabla_bienes_uso` y el API usa su `id_tipo_bien_uso`. Si se omite, `detalle` e `id_tipo_bien_uso` son obligatorios y el sistema puede crear o reutilizar el bien de uso.
- Para `concepto`, `detalle` es obligatorio.
- `alicuota` puede enviarse como porcentaje (`21`) o multiplicador (`1.21`).

Ejemplo de gasto existente:

```json
{
    "tipo": "gasto",
    "id": 8632,
    "cantidad": 1,
    "neto_uni": 780,
    "alicuota": 21
}
```

Ejemplo de gasto con alta automática:

```json
{
    "tipo": "gasto",
    "detalle": "Gasto creado por API",
    "cantidad": 1,
    "neto_uni": 780,
    "alicuota": 21
}
```

Ejemplo de bien de uso existente:

```json
{
    "tipo": "bien_uso",
    "id": 8,
    "cantidad": 1,
    "neto_uni": 1200,
    "alicuota": 21
}
```

Ejemplo de bien de uso con alta automática:

```json
{
    "tipo": "bien_uso",
    "detalle": "Notebook para administración",
    "id_tipo_bien_uso": 2,
    "cantidad": 1,
    "neto_uni": 1200,
    "alicuota": 21
}
```

Ejemplo combinado con todos los tipos:

```json
{
    "productos": [
        {
            "tipo": "producto",
            "id": 95,
            "cantidad": 1,
            "neto_uni": 1000,
            "alicuota": 21
        },
        {
            "tipo": "gasto",
            "id": 8632,
            "cantidad": 1,
            "neto_uni": 780,
            "alicuota": 21
        },
        {
            "tipo": "bien_uso",
            "id": 8,
            "cantidad": 1,
            "neto_uni": 1200,
            "alicuota": 21
        },
        {
            "tipo": "concepto",
            "detalle": "Concepto sin stock",
            "cantidad": 1,
            "neto_uni": 500,
            "alicuota": 21
        }
    ]
}
```

### Percepciones:

```json
{
    "percepciones": [
        {
            "id_percepcion": 3,
            "id_regimen": 0,
            "id_impuesto": 0,
            "monto": 150
        }
    ]
}
```

`id_percepcion` debe identificar un tipo de percepción vigente. `id_regimen` e `id_impuesto` son opcionales; si se informan deben existir, estar vigentes y corresponder al tipo de percepción. El impuesto se resuelve siempre desde `id_percepcion`.

### Bloque `pago` para `contado_mixto`:

El bloque `pago` es obligatorio cuando `forma_pago` es `contado_mixto`.

```json
{
    "pago": {
        "id_punto_venta": 9,
        "fecha": "2026-06-29",
        "id_moneda": 1,
        "cotizacion": 1,
        "efectivo": 1210,
        "observaciones": "Orden de pago generada por API",
        "transferencias": [],
        "transferencias_pendientes": [],
        "valores": [],
        "retenciones": []
    }
}
```

Reglas del bloque:

- `id_punto_venta` debe ser un talonario de orden de pago (`id_movimiento = 2`).
- El talonario debe tener la misma fiscalidad que la compra.
- El talonario debe corresponder al mismo `id_contribuyente` de la compra.
- La sucursal del talonario debe ser compatible con la sucursal del usuario de la API.
- La suma de `efectivo`, `transferencias[].monto`, los montos reales de `transferencias_pendientes[]` y `valores[]`, y `retenciones[].monto_retenido` debe coincidir con el total calculado de la compra. La operación se rechaza antes de cargar la compra si los importes no coinciden.

Transferencias nuevas:

```json
{
    "id_cuenta": 4,
    "fecha": "2026-06-29",
    "numero": "987654",
    "monto": 500
}
```

Transferencias pendientes:

```json
{
    "id_transferencia": 18
}
```

También puede enviarse como `ids_transferencias: [18, 19]`. El monto se toma del movimiento bancario pendiente y no puede informarse parcialmente.

Valores existentes:

```json
{
    "id_valor": 1570
}
```

El pago siempre utiliza el monto completo registrado para el valor; no se admiten imputaciones parciales. `monto` es opcional y, si se envía, debe coincidir con el monto registrado o la operación será rechazada. El valor debe existir, estar vigente y disponible.

Para emitir un cheque propio:

1. Consultar chequeras con `GET /api/v2/caja/chequeras`.
2. Emitir el cheque con `POST /api/v2/caja/valores/alta`.
3. Enviar el `id_valor` devuelto dentro de `pago.valores[]`.

Retenciones:

```json
{
    "id_retencion": 1,
    "id_regimen": 0,
    "id_ss": 0,
    "fecha": "2026-06-29",
    "imp_retencion": true,
    "punto_venta": 1,
    "numero": 123,
    "monto_sujeto": 1000,
    "monto_retenido": 50
}
```

`id_retencion`, `punto_venta` y `numero` pueden obtenerse de `GET /api/v2/caja/tipos_retencion?id_punto_venta_pago=...`. `id_regimen` se consulta en `GET /api/v2/impuestos/regimenes?id_tipo_retencion=...` y `id_ss` en `GET /api/v2/impuestos/sujetos_suspendidos`.

### Ejemplo `cuenta_corriente`:

```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"fecha_comprobante":"2026-06-29","id_proveedor":12,"forma_pago":"cuenta_corriente","id_comprobante":1,"id_tipo":1,"punto_venta":1,"numero":12345,"id_contribuyente":0,"productos":[{"tipo":"producto","id":95,"cantidad":1,"neto_uni":1000,"alicuota":21}]}' \
'https://cianbox.org/micuenta/api/v2/compras/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Ejemplo `contado_mixto`:

```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"fecha_comprobante":"2026-06-29","id_proveedor":12,"forma_pago":"contado_mixto","id_comprobante":1,"id_tipo":1,"punto_venta":1,"numero":12346,"id_contribuyente":0,"productos":[{"tipo":"producto","id":95,"cantidad":1,"neto_uni":1000,"alicuota":21}],"pago":{"id_punto_venta":9,"fecha":"2026-06-29","efectivo":1210,"transferencias":[],"valores":[],"retenciones":[]}}' \
'https://cianbox.org/micuenta/api/v2/compras/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_compras",
    "method": "POST",
    "body": {
        "status": "ok",
        "description": "La compra se cargó correctamente",
        "id": 321
    }
}
```

Para `contado_mixto`, la respuesta incluye la orden de pago creada:

```json
{
    "status": "ok",
    "description": "La compra se cargó correctamente",
    "id": 321,
    "id_pago": 654
}
```

### Webhooks

El recurso dispone del evento `compras`, cuyo `endpoint` es `compras`.

Se genera una notificación cuando:

- se carga una compra desde la interfaz o desde `POST /api/v2/compras/alta`;
- se modifican sus datos generales, fecha, numeración, proveedor, condición de pago, sucursal, cotización, impuestos u observaciones;
- se elimina una compra;
- una unificación de proveedores reasigna la compra;
- una importación de proveedores crea una compra por saldo inicial.

El webhook se configura con `POST /api/v2/general/notificaciones/alta`:

```json
{
    "evento": ["compras"],
    "url": "https://integracion.ejemplo.com/webhooks/cianbox"
}
```

Ejemplo del cuerpo enviado a la URL configurada:

```json
{
    "event": "compras",
    "created": "2026-07-20 14:30:00",
    "id": ["321"],
    "endpoint": "compras"
}
```

`id` siempre es un arreglo y puede incluir más de una compra. Para obtener el estado actualizado se debe consultar `GET /api/v2/compras?id=321`. En eliminaciones se debe usar `GET /api/v2/compras?id=321&vigente=all`, porque el listado predeterminado sólo devuelve compras vigentes.
