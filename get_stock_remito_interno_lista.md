### Descripción:

Obtiene un remito interno o lista de remitos internos de transferencia entre sucursales.

### URL:

`https://cianbox.org/{cuenta}/api/v2/stock/remito_interno`

o

`https://cianbox.org/{cuenta}/api/v2/stock/remito_interno/lista`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|access_token|SI|Token de acceso válido|
|id|NO|ID del/los remitos internos. Acepta uno o varios separados por coma|
|id_usuario_emitio|NO|Filtra por usuario que emitió/cargó el remito. También se acepta `id_usuario` por compatibilidad|
|id_usuario_recibio|NO|Filtra por usuario que recibió el remito|
|id_sucursal_origen|NO|Filtra por sucursal de origen|
|id_sucursal_destino|NO|Filtra por sucursal de destino|
|id_punto_venta|NO|Filtra por talonario|
|entregado|NO|Filtra por estado de recepción. Acepta `true` o `false`|
|fecha_desde|NO|Fecha mínima del comprobante (`YYYY-MM-DD`)|
|fecha_hasta|NO|Fecha máxima del comprobante (`YYYY-MM-DD`)|
|fecha_carga_desde|NO|Fecha mínima de carga (`YYYY-MM-DD`)|
|fecha_carga_hasta|NO|Fecha máxima de carga (`YYYY-MM-DD`)|
|fecha_recepcion_desde|NO|Fecha mínima de recepción (`YYYY-MM-DD`)|
|fecha_recepcion_hasta|NO|Fecha máxima de recepción (`YYYY-MM-DD`)|
|search|NO|Busca por número, observaciones, talonario, sucursales o usuario|
|page|NO|Página solicitada|
|limit|NO|Límite de ítems por petición. Máximo 200|
|fields|NO|Cualquiera de los listados en **available_fields** separados por comas. Por defecto devuelve el resumen sin `detalles`|
|order|NO|Ordena el listado. Acepta `create-date-asc`, `create-date-desc`, `modified-date-asc`, `modified-date-desc`, `id-asc`, `id-desc`|

### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/stock/remito_interno?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id=12345&fields=id,fecha,fecha_carga,fecha_entrega,fecha_recepcion,entregado,vigente,anulado,id_usuario_emitio,usuario_emitio,id_usuario_recibio,usuario_recibio,id_punto_venta,talonario,comprobante,punto_venta,numero,id_sucursal_origen,sucursal_origen,id_sucursal_destino,sucursal_destino,observaciones,detalles'
```

### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_stock",
    "method": "GET",
    "available_fields": [
        "id",
        "fecha",
        "fecha_carga",
        "fecha_entrega",
        "fecha_recepcion",
        "entregado",
        "vigente",
        "anulado",
        "id_usuario_emitio",
        "usuario_emitio",
        "id_usuario_recibio",
        "usuario_recibio",
        "id_punto_venta",
        "talonario",
        "comprobante",
        "punto_venta",
        "numero",
        "id_sucursal_origen",
        "sucursal_origen",
        "id_sucursal_destino",
        "sucursal_destino",
        "observaciones",
        "detalles"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 12345,
            "fecha": "2026-04-09",
            "fecha_carga": "2026-04-09 10:15:22",
            "fecha_entrega": "2026-04-09",
            "fecha_recepcion": "2026-04-09 13:42:11",
            "entregado": true,
            "vigente": true,
            "anulado": false,
            "id_usuario_emitio": 99,
            "usuario_emitio": "Usuario Demo",
            "id_usuario_recibio": 104,
            "usuario_recibio": "Operador Demo",
            "id_punto_venta": 7,
            "talonario": "REMITO INTERNO DEMO",
            "comprobante": "REM [X] 0007-00001234",
            "punto_venta": "0007",
            "numero": "00001234",
            "id_sucursal_origen": 1,
            "sucursal_origen": "Sucursal Depósito A",
            "id_sucursal_destino": 2,
            "sucursal_destino": "Sucursal Venta B",
            "observaciones": "Transferencia interna de ejemplo",
            "detalles": [
                {
                    "id": 50001,
                    "id_producto": 1001,
                    "detalle": "Producto de ejemplo sin serie",
                    "cantidad": 2,
                    "numeros_serie": []
                },
                {
                    "id": 50002,
                    "id_producto": 1002,
                    "detalle": "Producto de ejemplo con serie",
                    "cantidad": 1,
                    "numeros_serie": [
                        "SERIE-DEMO-0001"
                    ]
                }
            ]
        }
    ]
}
```

### Notas:

- Para incluir el detalle de productos, pedir `fields=...,detalles`.
- `fecha` corresponde a `fecha_comprobante`.
- `entregado=true` indica que el remito ya fue recibido en la sucursal destino.
