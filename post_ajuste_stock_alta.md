### Descripción:

Realiza un ajuste de stock en una sucursal, sobre varios productos

### URL:

`https://cianbox.org/{cuenta}/api/v2/productos/ajuste_stock/alta`

### Método: POST

### Parámetros:
```json
{
    "id_sucursal": 5,
    "id_usuario": 3,
    "ajustes": [
        {"id_producto": 265, "stock": 10.00},
        {"id_producto": 761, "stock": 2.00},
        {"id_producto": 17, "stock": 0.00}
    ]
}
```

### Ejemplo:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{ \
    "id_sucursal": 5,\
    "id_usuario": 3,\
    "ajustes": [\
        {"id_producto": 265, "stock": 10.00},\
        {"id_producto": 761, "stock": 2.00},\
        {"id_producto": 17, "stock": 0.00}\
    ]\
    }'\
'https://cianbox.org/micuenta/api/v2/productos/ajuste_stock/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_productos",
    "method": "POST",
    "body": {
        "status": "ok",
        "description": "El ajuste de stock se cargó correctamente"
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
