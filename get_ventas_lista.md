### Descripción:

Obtiene un venta o lista de ventas

### URL:

`https://cianbox.org/{cuenta}/api/v2/ventas`

o

`https://cianbox.org/{cuenta}/api/v2/ventas/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id de/las ventas ej. 1566 o 143,188,19        |
|cuit_emisor  |NO        |Número de CUIT del emisor. Se aceptan solo valores numéricos, sin puntos, guiones, etc.|
|numero_documento_venta |NO        |Número de documento del receptor. Se aceptan solo valores numéricos, sin puntos, guiones, etc.|
|vigente      |NO        |Filtrar por las ventas vigentes / no vigentes|
|anulado      |NO        |Filtrar por las ventas anuladas / no anuladas|
|limit        |NO        |Límite de ítems por petición                 |
|page         |NO        |Página solicitada|
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,razon|
|order        |NO        |Ordena el listado, acepta los valores: create-date-asc, create-date-desc, id-asc, id-desc|

### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/ventas?access_token=CBX_AT-TcIHdWOvdpIMNsXG...
```
### Respuesta:


```json
{
    "status": "ok",
    "scheme": "http",
    "host": "cianbox.test",
    "account": "micuenta",
    "module": "pv_ventas",
    "method": "GET",
    "timestamp": "2024-10-21 15:20:59",
       "available_fields": [
        "id",
        "fecha_carga",
        "fecha",
        "id_usuario",
        "cliente",
        "cuit_emisor",
        "punto_venta",
        "numero",
        "observaciones",
        "exento",
        "gravado",
        "iva",
        "no_gravado",
        "total",
        "facturado",
        "entregado",
        "fecha_entrega",
        "cta_cte",
        "id_usuario_cargo",
        "detalles",
        "id_forma_entrega",
        "anulado",
        "descuento",
        "afip_errores",
        "id_forma_pago",
        "id_moneda",
        "cotizacion",
        "id_canal_venta",
        "id_tipo_documento",
        "numero_documento_venta",
        "url",
        "sucursal",
        "vigente"
    ],
    "body": [
        {
            "id": 20220,
            "fecha_carga": "2024-10-23 13:00:02",
            "fecha": "2024-10-23",
            "id_usuario": "2",
            "cliente": [
                {
                    "id": "1",
                    "nombre": "Juan Ignacio Innomindado",
                    "razon": "Juan Ignacio Innomindado"
                }
            ],
            "cuit_emisor": "99999999999",
            "punto_venta": "0003",
            "numero": "00009000",
            "observaciones": "",
            "exento": "0.0000",
            "gravado": "5453.7200",
            "iva": "1145.2800",
            "no_gravado": "0.0000",
            "total": "6599.0000",
            "facturado": "0",
            "entregado": "1",
            "fecha_entrega": "2024-10-23",
            "cta_cte": "0",
            "id_usuario_cargo": "0",
            "detalles": [
                {
                    "id": 1,
                    "id_producto": "34",
                    "detalle": " CUENTOS PARA DORMIR VOLUMEN 1",
                    "cantidad": "1.0000",
                    "alicuota": "1.2100",
                    "total": "6599.0000",
                    "precio_unico": "1"
                }
            ],
            "id_forma_entrega": "8",
            "anulado": "0",
            "descuento": "0.0000",
            "afip_errores": "",
            "id_forma_pago": "5",
            "id_moneda": "1",
            "cotizacion": "1.0000",
            "id_canal_venta": "5",
            "id_tipo_documento": "3",
            "numero_documento_venta": "99999999",
            "url": ["https://cianbox.org/bCswbVFP....RDJpYTc/res/f.php"],
            "sucursal": "Casa centrar",
            "vigente": "1"
        }
    ]
}
```
