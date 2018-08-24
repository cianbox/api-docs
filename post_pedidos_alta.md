### Descripción:

Crea un nuevo pedido

### URL:

`https://cianbox.org/{cuenta}/api/v2/pedidos/alta`

### Método: POST

### Parámetros:
```json
{
    "fecha": "2016-02-17",
    "id_canal": 6,
    "id_cuenta": 1,
    "id_cliente": 45,
    "id_usuario": 12,
    "observaciones": "Observaciones del pedido",
    "productos": [
        {
            "id": 67,
            "cantidad": 1.0000,
            "alicuota": 21.0000,
            "neto_uni": 974.2500
        },
        {
            "id": 256,
            "cantidad": 2.0000,
            "alicuota": 21.0000,
            "neto_uni": 419.0000
        }
    ]
}
```

### Ejemplo:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"fecha":"2018-08-23","id_canal":6,"id_cuenta":1,"id_cliente":1300,"id_usuario":41, \
"observaciones":"","productos":[ \
{"id":1791,"cantidad":1,"alicuota":21,"neto_uni":350}, \
{"id":2035,"cantidad":1,"alicuota":10.5,"neto_uni":284.3116}, \
{"id":2164,"cantidad":1,"alicuota":10.5,"neto_uni":1550.5638}, \
{"id":2685,"cantidad":1,"alicuota":10.5,"neto_uni":1803.2}]}' \
'https://cianbox.org/micuenta/api/v2/pedidos/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_pedidos",
    "method": "POST",
    "body": {
        "status": "ok",
        "description": "El pedido se cargó correctamente",
        "id": 321,
        "numero": 304
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
|id            |ID del pedido|
|numero        |Número del pedido|