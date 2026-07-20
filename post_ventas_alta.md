### Descripción:

Crea una nueva venta reutilizando el circuito real del sistema. Soporta venta directa, facturación de pedido y facturación de venta de Mercado Libre.

### URL:

`https://cianbox.org/{cuenta}/api/v2/ventas/alta`

### Método: POST

### Payload base:
```json
{
    "fecha": "2026-04-01",
    "origen": {
        "tipo": "directa"
    },
    "id_cliente": 256,
    "id_canal_venta": 1,
    "forma_pago": "cuenta_corriente",
    "id_punto_venta": 1,
    "id_moneda": 1,
    "cotizacion": 1,
    "observaciones": "Venta generada por integracion API",
    "fecha_vencimiento": "2026-04-30",
    "entrega": {
        "id_pv_remito": 0,
        "id_domicilio_entrega": 0,
        "id_empresa_transporte": 0,
        "cantidad_bultos": 0,
        "observaciones_remito": ""
    },
    "productos": [
        {
            "id": 95,
            "cantidad": 1,
            "neto_uni": 16211,
            "alicuota": 21
        }
    ],
    "percepciones": []
}
```

### Formas de pago soportadas:

|Valor|Descripción|
|---|---|
|`cuenta_corriente`|Genera la venta en cuenta corriente|
|`contado_mixto`|Genera la venta y luego un recibo/cobro imputando la misma venta|
|`efectivo`|Genera la venta cobrada en efectivo|
|`tarjeta_credito`|Requiere bloque `tarjeta`|
|`tarjeta_debito`|Requiere bloque `tarjeta`|
|`financiacion_propia`|Requiere bloque `financiacion`|

### Orígenes soportados:

|Campo|Uso|
|---|---|
|`tipo = "directa"`|Venta normal con `productos[]` obligatorios|
|`tipo = "pedido"`|Debe informar `id_pedido`; los ítems se reconstruyen desde el pedido|
|`tipo = "mercadolibre"`|Debe informar `id_venta_ml`; los ítems se reconstruyen desde la venta de ML. `id_cliente` puede omitirse si la venta de ML tiene datos suficientes para detectar o crear el cliente. `forma_pago` y, si corresponde, `tarjeta.*` deben venir siempre por payload. `entrega.id_pv_remito` no toma defaults desde la configuración de ML|

### Bloques condicionales:

#### `tarjeta`

Se usa con `forma_pago = "tarjeta_credito"` o `forma_pago = "tarjeta_debito"`.

```json
{
    "tarjeta": {
        "id_tarjeta": 32,
        "id_entidad": 1,
        "cuotas": 2,
        "cupon": "998877",
        "numero_lote": "77"
    }
}
```

#### `financiacion`

Se usa con `forma_pago = "financiacion_propia"`.

```json
{
    "financiacion": {
        "entrega": 1000,
        "periodicidad": "mensual",
        "cuotas": 3,
        "primer_vencimiento": "2026-05-10",
        "dia_vencimiento": 10,
        "dia_semana": "monday",
        "dia_anio": "10/05",
        "codigo_autorizacion": "AUT-123"
    }
}
```

#### `cobro`

Se usa con `forma_pago = "contado_mixto"`.

```json
{
    "cobro": {
        "id_punto_venta": 7,
        "fecha": "2026-04-01",
        "observaciones": "Cobro contado mixto",
        "efectivo": 10000,
        "tarjetas": [
            {
                "tipo": "credito",
                "id_tarjeta": 32,
                "id_entidad": 1,
                "cuotas": 2,
                "cupon": "551122",
                "numero_lote": "88",
                "monto": 9615.31
            }
        ],
        "depositos": [],
        "retenciones": [],
        "valores": []
    }
}
```

### Reglas importantes:

- `id_punto_venta` es obligatorio y siempre se numera automáticamente.
- La factura electrónica se genera siempre en forma diferida.
- Las percepciones automáticas no se resuelven dentro del alta. Deben obtenerse antes con `POST /api/v2/ventas/percepciones/preview`.
- `percepciones[]` es opcional y puede incluir percepciones manuales o las obtenidas desde el preview.
- `entrega.id_pv_remito = 0` (o el campo omitido) significa remito interno. Si la venta tiene ítems que mueven stock, el sistema genera igualmente el remito con `id_punto_venta = 0`.
- `entrega.id_pv_remito > 0` usa un talonario real de remito.
- `entrega.id_pv_remito = "pendiente"` no genera remito y no mueve stock.
- `entrega.id_pv_remito = "no_stock"` no genera remito y no mueve stock.
- En `contado_mixto`, `cobro.id_punto_venta` debe ser un talonario de cobros/recibos y debe coincidir en fiscalidad con la venta.
- La suma de `efectivo + tarjetas + depositos + retenciones + valores` debe ser igual al total final de la venta.
- `cobro.depositos[]` usa el shape (`id_cuenta`, `fecha`, `numero`, `monto`) y cubre tanto depósitos como transferencias bancarias.
- `cobro.transferencias[]` ya no forma parte del contrato público y devuelve error. Todos los movimientos bancarios deben informarse en `cobro.depositos[]`.
- `cobro.retenciones[]` requiere `id_retencion` o `id_tipo_retencion`, `punto_venta`, `numero`, `monto_sujeto` y `monto_retenido`. Los demás campos son opcionales.
- `cobro.valores[]` requiere `id_entidad`, `numero_cheque`, `fecha_cheque`, `fecha_vencimiento` y `monto`. Los demás campos del cheque/valor son opcionales.
- `forma_pago = "tarjeta_credito"` y `forma_pago = "tarjeta_debito"` persisten el dato de la tarjeta en la venta, no generan recibo.
- `forma_pago = "financiacion_propia"` genera la estructura de cuotas en cuenta corriente según el bloque `financiacion`.

### Casos de uso

#### 1. Venta directa en cuenta corriente
```json
{
    "fecha": "2026-04-01",
    "origen": { "tipo": "directa" },
    "id_cliente": 256,
    "id_canal_venta": 1,
    "forma_pago": "cuenta_corriente",
    "id_punto_venta": 1,
    "id_moneda": 1,
    "cotizacion": 1,
    "productos": [
        { "id": 95, "cantidad": 1, "neto_uni": 16211, "alicuota": 21 }
    ],
    "percepciones": []
}
```

#### 2. Venta directa con percepciones manuales
```json
{
    "fecha": "2026-04-01",
    "origen": { "tipo": "directa" },
    "id_cliente": 257,
    "id_canal_venta": 1,
    "forma_pago": "cuenta_corriente",
    "id_punto_venta": 1,
    "id_moneda": 1,
    "cotizacion": 1,
    "productos": [
        { "id": 95, "cantidad": 1, "neto_uni": 16211, "alicuota": 21 }
    ],
    "percepciones": [
        {
            "id_tipo_percepcion": 1,
            "id_regimen": 0,
            "id_impuesto": 4,
            "base_imponible": 16211,
            "monto": 100,
            "alicuota": 0.6169
        }
    ]
}
```

#### 3. Facturación de pedido
```json
{
    "fecha": "2026-04-01",
    "origen": {
        "tipo": "pedido",
        "id_pedido": 77416
    },
    "id_cliente": 256,
    "id_canal_venta": 1,
    "forma_pago": "cuenta_corriente",
    "id_punto_venta": 1,
    "id_moneda": 1,
    "cotizacion": 1,
    "percepciones": []
}
```

#### 4. Facturación de venta de Mercado Libre
```json
{
    "fecha": "2026-04-01",
    "origen": {
        "tipo": "mercadolibre",
        "id_venta_ml": 427496
    },
    "forma_pago": "tarjeta_credito",
    "id_punto_venta": 67,
    "entrega": {
        "id_pv_remito": 0
    },
    "tarjeta": {
        "id_tarjeta": 32,
        "id_entidad": 1,
        "cuotas": 1,
        "cupon": "ML-427496",
        "numero_lote": "1"
    },
    "percepciones": []
}
```

#### 5. Venta con tarjeta de crédito
```json
{
    "fecha": "2026-04-01",
    "origen": { "tipo": "directa" },
    "id_cliente": 256,
    "id_canal_venta": 1,
    "forma_pago": "tarjeta_credito",
    "id_punto_venta": 4,
    "id_moneda": 1,
    "cotizacion": 1,
    "productos": [
        { "id": 95, "cantidad": 1, "neto_uni": 16211, "alicuota": 21 }
    ],
    "tarjeta": {
        "id_tarjeta": 32,
        "id_entidad": 1,
        "cuotas": 2,
        "cupon": "998877",
        "numero_lote": "77"
    }
}
```

#### 6. Venta con tarjeta de débito
```json
{
    "fecha": "2026-04-01",
    "origen": { "tipo": "directa" },
    "id_cliente": 256,
    "id_canal_venta": 1,
    "forma_pago": "tarjeta_debito",
    "id_punto_venta": 4,
    "id_moneda": 1,
    "cotizacion": 1,
    "productos": [
        { "id": 95, "cantidad": 1, "neto_uni": 16211, "alicuota": 21 }
    ],
    "tarjeta": {
        "id_tarjeta": 32,
        "id_entidad": 1,
        "cuotas": 1,
        "cupon": "998878",
        "numero_lote": "78"
    }
}
```

#### 7. Venta con financiación propia
```json
{
    "fecha": "2026-04-01",
    "origen": { "tipo": "directa" },
    "id_cliente": 256,
    "id_canal_venta": 1,
    "forma_pago": "financiacion_propia",
    "id_punto_venta": 4,
    "id_moneda": 1,
    "cotizacion": 1,
    "productos": [
        { "id": 95, "cantidad": 1, "neto_uni": 16211, "alicuota": 21 }
    ],
    "financiacion": {
        "entrega": 1000,
        "periodicidad": "mensual",
        "cuotas": 3,
        "primer_vencimiento": "2026-05-10",
        "dia_vencimiento": 10,
        "dia_semana": "monday",
        "dia_anio": "10/05",
        "codigo_autorizacion": "AUT-123"
    }
}
```

#### 8. Venta con contado mixto simple
```json
{
    "fecha": "2026-04-01",
    "origen": { "tipo": "directa" },
    "id_cliente": 257,
    "id_canal_venta": 1,
    "forma_pago": "contado_mixto",
    "id_punto_venta": 1,
    "id_moneda": 1,
    "cotizacion": 1,
    "productos": [
        { "id": 95, "cantidad": 1, "neto_uni": 16211, "alicuota": 21 }
    ],
    "percepciones": [],
    "cobro": {
        "id_punto_venta": 7,
        "fecha": "2026-04-01",
        "efectivo": 10000,
        "tarjetas": [
            {
                "tipo": "credito",
                "id_tarjeta": 32,
                "id_entidad": 1,
                "cuotas": 2,
                "cupon": "551122",
                "numero_lote": "88",
                "monto": 9615.31
            }
        ],
        "depositos": [],
        "retenciones": [],
        "valores": []
    }
}
```

#### 9. Venta con contado mixto completo
```json
{
    "fecha": "2026-04-01",
    "origen": { "tipo": "directa" },
    "id_cliente": 257,
    "id_canal_venta": 1,
    "forma_pago": "contado_mixto",
    "id_punto_venta": 1,
    "id_moneda": 1,
    "cotizacion": 1,
    "productos": [
        { "id": 95, "cantidad": 1, "neto_uni": 16211, "alicuota": 21 }
    ],
    "percepciones": [],
    "cobro": {
        "id_punto_venta": 7,
        "fecha": "2026-04-01",
        "efectivo": 3000,
        "tarjetas": [
            {
                "tipo": "credito",
                "id_tarjeta": 32,
                "id_entidad": 1,
                "cuotas": 2,
                "cupon": "771199",
                "numero_lote": "991",
                "monto": 5000
            }
        ],
        "depositos": [
            {
                "id_cuenta": 1,
                "fecha": "2026-04-01",
                "numero": "22334",
                "monto": 2000
            },
            {
                "id_cuenta": 1,
                "fecha": "2026-04-01",
                "numero": "33445",
                "monto": 4000
            }
        ],
        "retenciones": [
            {
                "id_retencion": 1,
                "fecha": "2026-04-01",
                "fecha_afec": "2026-04-01",
                "punto_venta": 1,
                "numero": 12345678,
                "monto_sujeto": 19615.31,
                "monto_retenido": 3115.31
            }
        ],
        "valores": [
            {
                "id_entidad": 1,
                "sucursal": 0,
                "codigo_postal": 0,
                "emitio": "API TEST",
                "cuit_emitio": "20123456789",
                "numero_cheque": "44556677",
                "numero_cuenta": 123456,
                "fecha_cheque": "2026-04-01",
                "fecha_vencimiento": "2026-04-15",
                "no_a_la_orden": false,
                "echeque": false,
                "cruzado": false,
                "monto": 2500
            }
        ]
    }
}
```

### Ejemplo genérico con `curl`
```bash
curl -X POST -H "Content-Type: application/json" \
-d '<payload del caso de uso elegido>' \
'https://cianbox.org/micuenta/api/v2/ventas/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:
```json
{
    "status": "ok",
    "scheme": "http",
    "host": "cianbox.test",
    "account": "micuenta",
    "module": "pv_ventas",
    "method": "POST",
    "body": {
        "status": "ok",
        "description": "La venta se cargo correctamente",
        "id": 565738,
        "id_recibo": 600922
    }
}
```

|Valor|Descripción|
|---|---|
|`status`|Estado de la petición: **ok** o **error**|
|`description`|Descripción del resultado|
|`id`|ID de la venta|
|`id_recibo`|ID del recibo/cobro generado cuando `forma_pago = contado_mixto`|

### Webhooks

- El alta de venta dispara el evento `ventas`.
- Las modificaciones principales de ventas y remitos vinculados también disparan el evento `ventas`.
- El alta del webhook se realiza desde el módulo de notificaciones de API usando `evento = ["ventas"]`.
