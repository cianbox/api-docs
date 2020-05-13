### Descripción:

Editar un estado de pedido

### URL:

`https://cianbox.org/{cuenta}/api/v2/pedidos/estados/editar`

### Método: PUT

### Parámetros:

#### vía URL
|Parámetro    |Requerido |Descripción            |
|-------------|----------|-----------------------|
|access_token |SI        |Token de acceso válido |
|id           |SI        |id del estado a editar |

#### vía JSON
``` json
{
    "estado": "Preparando Mercadería"
}
```

### Ejemplo:
``` sh
curl -X PUT -H "Content-Type: application/json" \
-d '{ \
        "estado": "Preparando Mercadería" \
    }' \
'https://cianbox.org/micuenta/api/v2/pedidos/estados/editar?id=5&access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:
``` json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_pedidos",
    "method": "PUT",
    "body": {
        "status": "ok",
        "description": "El estado se actualizó correctamente",
        "id": 5
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
|id            |ID del estado actualizado|