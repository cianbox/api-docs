### Descripción:

Crea un nuevo estado de pedido

### URL:

`https://cianbox.org/{cuenta}/api/v2/pedidos/estados/alta`

### Método: POST

### Parámetros:
```json
{
    "estado": "En Preparación"
}
```

### Ejemplo:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{ \
        "estado": "En Preparación" \
    }' \
'https://cianbox.org/micuenta/api/v2/pedidos/estados/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
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
        "description": "El estado se cargó con éxito",
        "id": 5
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
|id            |ID del estado|