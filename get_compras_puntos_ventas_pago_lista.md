### Descripción:

Obtiene los talonarios/puntos de venta disponibles para generar órdenes de pago desde compras.

Este endpoint se usa principalmente para completar `pago.id_punto_venta` cuando `POST /api/v2/compras/alta` se envía con `forma_pago = contado_mixto`.

### URL:

`https://cianbox.org/{cuenta}/api/v2/compras/puntos_ventas_pago`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|access_token|SI|Token de acceso válido|
|id|NO|Filtra por uno o más puntos de venta|
|id_sucursal|NO|Filtra por sucursal. Si se omite usa la sucursal del usuario de la API|
|id_contribuyente|NO|Filtra por contribuyente fiscal. `0` representa el contribuyente principal|
|fiscal|NO|`true` o `false`|
|id_comprobante_compra|NO|Junto con `id_tipo_compra`, filtra talonarios con la misma fiscalidad que la compra|
|id_tipo_compra|NO|Junto con `id_comprobante_compra`, filtra talonarios con la misma fiscalidad que la compra|
|search|NO|Busca por talonario, comprobante, tipo o punto de venta|
|page|NO|Página solicitada|
|limit|NO|Límite de ítems por petición. Máximo: 200|
|fields|NO|Campos de `available_fields` separados por coma|
|order|NO|Acepta `name-asc`, `name-desc`, `id-asc`, `id-desc`|

### Ejemplo:

```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/compras/puntos_ventas_pago?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_contribuyente=0&id_comprobante_compra=1&id_tipo_compra=1'
```

### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_compras",
    "method": "GET",
    "available_fields": [
        "id",
        "id_sucursal",
        "id_comprobante",
        "comprobante",
        "id_tipo",
        "tipo",
        "talonario",
        "punto_venta",
        "fiscal",
        "id_contribuyente",
        "descripcion",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 9,
            "id_sucursal": 1,
            "id_comprobante": 15,
            "comprobante": "ODP",
            "id_tipo": 1,
            "tipo": "A",
            "talonario": "Orden de Pago",
            "punto_venta": "0001",
            "fiscal": true,
            "id_contribuyente": 0,
            "descripcion": "[Orden de Pago] ODP [A] 0001",
            "vigente": true
        }
    ]
}
```

### Uso en `contado_mixto`:

El `id` devuelto se envía como `pago.id_punto_venta`.

```json
{
    "forma_pago": "contado_mixto",
    "id_contribuyente": 0,
    "pago": {
        "id_punto_venta": 9,
        "efectivo": 1210,
        "transferencias": [],
        "valores": [],
        "retenciones": []
    }
}
```
