### Descripción:

Obtiene una compra o lista de compras.

### URL:

`https://cianbox.org/{cuenta}/api/v2/compras`

o

`https://cianbox.org/{cuenta}/api/v2/compras/lista`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|access_token|SI|Token de acceso válido|
|id|NO|id de la/las compras, por ejemplo `1566` o `143,188,19`|
|id_proveedor|NO|Filtra por uno o más proveedores|
|id_contribuyente|NO|Filtra por contribuyente fiscal de la compra. `0` representa el contribuyente principal|
|numero_documento_proveedor|NO|Filtra por CUIT/documento del proveedor|
|id_comprobante|NO|Filtra por uno o más tipos de comprobante|
|id_tipo|NO|Filtra por uno o más tipos/letras|
|punto_venta|NO|Filtra por punto de venta|
|numero|NO|Filtra por número de comprobante|
|id_sucursal|NO|Filtra por una o más sucursales|
|fecha_carga_desde|NO|Fecha de carga desde, formato `YYYY-MM-DD`|
|fecha_carga_hasta|NO|Fecha de carga hasta, formato `YYYY-MM-DD`|
|fecha_comprobante_desde|NO|Fecha de comprobante desde, formato `YYYY-MM-DD`|
|fecha_comprobante_hasta|NO|Fecha de comprobante hasta, formato `YYYY-MM-DD`|
|fecha_contabilizacion_desde|NO|Fecha de contabilización desde, formato `YYYY-MM-DD`|
|fecha_contabilizacion_hasta|NO|Fecha de contabilización hasta, formato `YYYY-MM-DD`|
|vigente|NO|`true`, `false` o `all`. Predeterminado: `true`|
|page|NO|Página solicitada|
|limit|NO|Límite de ítems por petición. Máximo: 200|
|fields|NO|Campos de `available_fields` separados por coma|
|order|NO|Acepta `create-date-asc`, `create-date-desc`, `id-asc`, `id-desc`|

### Ejemplo:

```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/compras?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&fecha_comprobante_desde=2026-06-01&fields=id,fecha_comprobante,proveedor,numero_comprobante,total,detalles'
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
        "fecha_carga",
        "fecha_comprobante",
        "fecha_contabilizacion",
        "id_usuario",
        "usuario",
        "id_proveedor",
        "proveedor",
        "id_contribuyente",
        "contribuyente",
        "id_movimiento",
        "movimiento",
        "id_comprobante",
        "comprobante",
        "id_tipo",
        "tipo",
        "punto_venta",
        "numero",
        "numero_comprobante",
        "id_moneda",
        "cotizacion",
        "gravado",
        "no_gravado",
        "exento",
        "iva",
        "percepcion_iibb",
        "percepcion_iva",
        "percepcion_otras",
        "imp_internos",
        "total",
        "ctacte",
        "saldo",
        "pagado",
        "fecha_vencimiento",
        "observaciones",
        "id_categoria",
        "categoria",
        "id_sucursal",
        "vigente",
        "detalles"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 321,
            "fecha_comprobante": "2026-06-29",
            "proveedor": "Proveedor SRL",
            "id_contribuyente": 0,
            "contribuyente": "Empresa Demo SA",
            "numero_comprobante": "FAC [A] 0001-00012345",
            "total": 1210,
            "detalles": [
                {
                    "id": 900,
                    "tipo": "producto",
                    "id_producto": 95,
                    "detalle": "Producto de prueba",
                    "cantidad": 1,
                    "alicuota": 1.21,
                    "gravado": 1000,
                    "iva": 210,
                    "total": 1210
                }
            ]
        }
    ]
}
```
