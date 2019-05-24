### Descripción:

Da de baja un webhook relacionado a uno o más eventos

### URL:

`https://cianbox.org/{cuenta}/api/v2/notificaciones`

o

`https://cianbox.org/{cuenta}/api/v2/notificaciones/eliminar`

### Método: DELETE

### Parámetros:
```json
{
    "evento": ["clientes", "pedidos"]
}
```
> La variable evento puede ser un array con los nombres de los eventos o un string "all" para asignar a todos los eventos

> Los eventos disponibles son: clientes, pedidos, productos, categorias, marcas, listas_precio, sucursales, cotizaciones

### Ejemplo:
```bash
curl -X DELETE -H "Content-Type: application/json" \
-d '{ \
        "evento": ["productos", "marcas", "categorias"] \
    }' \
'https://cianbox.org/micuenta/api/v2/notificaciones?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
```bash
curl -X DELETE -H "Content-Type: application/json" \
-d '{ \
        "evento": "all" \
    }' \
'https://cianbox.org/micuenta/api/v2/notificaciones/eliminar?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "gr_config",
    "method": "DELETE",
    "body": {
        "status": "ok",
        "descripcion": "La url se eliminó con éxito"
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|