### Descripción:

Asigna un webhook a un evento

### URL:

`https://cianbox.org/{cuenta}/api/v2/general/notificaciones/alta`

### Método: POST

### Parámetros:
```json
{
    "evento": ["clientes", "pedidos"],
    "url": "http://urldeejemplo.com.ar/ntf.php"
}
```
> La variable evento puede ser un array con los nombres de los eventos o un string "all" para asignar a todos los eventos

> Los eventos disponibles son: clientes, pedidos, productos, categorias, marcas, listas_precio, sucursales, cotizaciones

### Ejemplo:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{ \
        "evento": ["productos", "marcas", "categorias"], \
        "url": "http://urldeejemplo.com.ar/ntf.php" \
    }' \
'https://cianbox.org/micuenta/api/v2/general/notificaciones/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{ \
        "evento": "all", \
        "url": "http://urldeejemplo.com.ar/ntf.php" \
    }' \
'https://cianbox.org/micuenta/api/v2/general/notificaciones/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "gr_config",
    "method": "POST",
    "body": {
        "status": "ok",
        "descripcion": "La url se informó con éxito"
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|