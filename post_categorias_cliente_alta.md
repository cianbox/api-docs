### Descripción:

Crea una nueva categoría de cliente

### URL:

`https://cianbox.org/{cuenta}/api/v2/clientes/categorias/alta`

### Método: POST

### Parámetros:
```json
{
    "categoria": "FERRETERIA"
}
```

### Ejemplo:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{ \
        "categoria": "FERRETERIA"
    }' \
'https://cianbox.org/micuenta/api/v2/clientes/categorias/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_clientes",
    "method": "POST",
    "body": {
        "status": "ok",
        "description": "Categorias: 1 nueva(s) y 0 editada(s)",
        "id": 20
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
|id            |ID de la categoría de cliente|