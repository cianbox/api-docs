### Descripción:

Obtiene un pedido o lista de pedidos

### URL:

`https://cianbox.org/{cuenta}/api/v2/pedidos`

o

`https://cianbox.org/{cuenta}/api/v2/pedidos/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id del/los pedidos ej. 1566 o 143,188,19      |
|page         |NO        |Página solicitada                             |
|limit        |NO        |Límite de ítems por petición                  |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,numero|
|order        |NO        |Ordena el listado, acepta los valores: create-date-asc, create-date-desc, modified-date-asc, modified-date-desc, id-asc, id-desc|


### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/pedidos?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_pedidos",
    "method": "GET",
    "available_fields": [
        "id",
        "updated",
        "fecha",
        "vendedor",
        "numero",
        "id_cliente",
        "id_usuario_externo",
        "cliente",
        "encargado",
        "localidad",
        "neto",
        "total",
        "observaciones",
        "transporte",
        "facturado",
        "cobrado",
        "estado",
        "entregado",
        "zona_cliente",
        "detalles",
        "anulado",
        "vigente",
        "id_moneda",
        "cotizacion"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 318,
            "updated": "2018-08-23 14:47:34",
            "fecha": "2018-08-23",
            "vendedor": "Bilbo Bolsón",
            "numero": "00000318",
            "id_cliente": 19,
            "id_usuario_externo": 41,
            "cliente": "Juan Ignacio Innominado",
            "encargado": "",
            "localidad": "Rio Primero (CBA)",
            "neto": 350,
            "total": 423.5,
            "observaciones": "",
            "transporte": "",
            "facturado": "Pendiente",
            "cobrado": 0,
            "estado": "LISTO PARA FACTURAR",
            "entregado": 0,
            "zona_cliente": "",
            "detalles": [
                {
                    "id": 435,
                    "id_producto": 1791,
                    "detalle": "ACTUALIZACION DE GPS GARMIN",
                    "cantidad": 1,
                    "alicuota": 1.21,
                    "neto_uni": 350
                }
            ],
            "anulado": false,
            "vigente": true,
            "id_moneda": 1,
            "cotizacion": 1.00
        }
    ]
}
```