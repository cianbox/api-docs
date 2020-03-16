### Descripción:

Da de baja un estado de pedido

### URL:

`https://cianbox.org/{cuenta}/api/v2/pedidos/estados`

o

`https://cianbox.org/{cuenta}/api/v2/pedidos/estados/eliminar`

### Método: DELETE

### Parámetros:
|Parámetro    |Requerido |Descripción              |
|-------------|----------|-------------------------|
|access_token |SI        |Token de acceso válido   |
|id           |SI        |id del estado a eliminar |

### Ejemplo:
```bash
curl -X DELETE 'https://cianbox.org/micuenta/api/v2/pedidos/estados?id=5&access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_pedidos",
    "method": "DELETE",
    "body": {
        "status": "ok",
        "descripcion": "El estado se eliminó con éxito",
        "id": 5
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
|id            |ID del estado eliminado|