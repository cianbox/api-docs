### Descripción:

Editar una categoría de cliente

### URL:

`https://cianbox.org/{cuenta}/api/v2/clientes/categorias/editar`

### Método: PUT

### Parámetros:

#### vía URL
|Parámetro    |Requerido |Descripción             |
|-------------|----------|------------------------|
|access_token |SI        |Token de acceso válido  |
|id           |SI        |id de la categoría a editar |

#### vía JSON
``` json
{
    "categoria": "FERRETERIA"
}
```

### Ejemplo:
``` sh
curl -X PUT -H "Content-Type: application/json" \
-d '{ \
        "categoria": "FERRETERIA"
    }' \
'https://cianbox.org/micuenta/api/v2/clientes/categorias/editar?id=2&access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:
``` json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_clientes",
    "method": "PUT",
    "body": {
        "status": "ok",
        "description": "Categorias: 0 nueva(s) y 1 editada(s)",
        "id": 2
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
|id            |ID de la categoría de cliente actualizada|