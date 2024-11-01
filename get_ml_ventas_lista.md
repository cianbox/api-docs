### Descripción:

Obtiene una venta o lista de ventas

### URL:

`http://cianbox.test/{cuenta}/api/v2/mercadolibre/ventas `

o

`http://cianbox.test/{cuenta}/api/v2/mercadolibre/ventas/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id_usuario_externo |NO        |id del usuario que provee MercadoLibre ej. 99161998 o 99161998, 99161999 |
|id_venta_ml        |NO        |Filtra por id de venta traído de ML ej. 2000006295990422 o 2000006295990422, 2000006295990423 |
|id_user_ml         |NO        |Filtra por id de la cuenta (integración) brindado por MercadoLibre. Ej: 9999 o 9998, 9999 |
|id_publicacion_ml  |NO        |Filtra por id de la publicacion ML ej. MLA1408999998 o MLA1408999998, MLA1408999999 |
|vigente      |NO        |Filtrar por las ventas vigentes / no vigentes |
|cancelada    |NO        |Filtrar por las ventas canceladas             |
|limit        |NO        |Límite de ítems por petición                  |
|page         |NO        |Página solicitada                             |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,razon |
|order        |NO        |Ordena el listado, acepta los valores: create-date-asc, create-date-desc, update-date-asc, update-date-desc, id-asc, id-desc, id_venta_ml-asc, id_venta_ml-desc |

### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/mercadolibre/ventas?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:

```json

{
    "status": "ok",
    "scheme": "http",
    "host": "cianbox.test",
    "account": "micuenta",
    "module": "ml_ventas",
    "method": "GET",
    "timestamp": "2024-10-21 16:49:40",
    "available_fields": [
        "id",
        "id_venta_ml",
        "id_envio_ml",
        "id_pack_ml",
        "id_publicacion_ml",
        "detalle",
        "id_usuario_externo",
        "razon",
        "id_condicion",
        "numero_documento",
        "domicilio",
        "localidad",
        "email",
        "envio",
        "recibe_envio",
        "fecha_creacion",
        "fecha_cierre",
        "cantidad",
        "precio_unitario",
        "comision",
        "total_cupones",
        "total",
        "cobrado",
        "despachado",
        "recibido",
        "completado",
        "id_venta_facturador",
        "id_cliente",
        "created",
        "first_notified",
        "updated",
        "cancelada",
        "motivo_cancelada",
        "costo_envio",
        "costo_envio_vendedor",
        "logistica",
        "canal_venta",
        "detalles_cuenta_ml",
        "reservas_canceladas",
        "vigente"
    ],
    "body": [
        {
            "id": 25422,
            "id_venta_ml": "2000009999999999",
            "id_envio_ml": "99999999999",
            "id_pack_ml": "",
            "id_publicacion_ml": "MLA1408999999",
            "detalle": {
                "id": 25465,
                "id_variante": "9999",
                "cantidad": "1",
                "precio_unitario": "55399.0000",
                "productos_publicacion": [
                    {
                        "id_producto": 999,
                        "cantidad": 1,
                        "monto": 55399
                    }
                ],
                "vigente": "1"
            },
            "id_usuario_externo": "1",
            "razon": "Juan Ignacio Innomindado",
            "id_condicion": "4",
            "numero_documento": "30999999991",
            "domicilio": "San Martín 1234",
            "localidad": "Quilmes Oeste Buenos Aires",
            "email": "",
            "envio": "Prioritario a domicilio",
            "recibe_envio": "",
            "fecha_creacion": "2024-10-17 14:38:12",
            "fecha_cierre": "2024-10-17 14:38:13",
            "cantidad": "1.0000",
            "precio_unitario": "13299.0000",
            "comision": "3994.3400",
            "total_cupones": "0.0000",
            "total": "13299.0000",
            "cobrado": "1",
            "despachado": "0",
            "recibido": "0",
            "completado": "0",
            "id_venta_facturador": "0",
            "id_cliente": "0",
            "created": "2024-10-17 01:38:44",
            "first_notified": "",
            "updated": "2024-10-17 02:03:33",
            "cancelada": "0",
            "motivo_cancelada": "",
            "costo_envio": "2289.9900",
            "costo_envio_vendedor": "0.0000",
            "logistica": "self_service",
            "canal_venta": "marketplace",
            "detalles_cuenta_ml": {
                "cuenta": "micuenta (mercadolibre@micuenta.com.ar)",
                "user": "micuenta"
            },
            "reservas_canceladas": "0",
            "vigente": "1"
        }
    ]
}
```
