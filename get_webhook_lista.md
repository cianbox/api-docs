### Descripción:

Obtiene las Listas de Precio

### URL:

`https://cianbox.org/{cuenta}/api/v2/general/notificaciones`

o

`https://cianbox.org/{cuenta}/api/v2/general/notificaciones/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id de los eventos ej. 2 o 1,3,4               |
|evento       |NO        |nombres de los eventos ej. producto o clientes,marca,categoria |

> *Nota:* Se puede filtrar por id o por evento, pero no por los dos a la vez
> Los eventos disponibles son: clientes, pedidos, productos, categorias, marcas, listas_precio, sucursales, cotizaciones 

### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/general/notificaciones?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "gr_config",
    "method": "GET",
    "body": [
        {
            "id": 1,
            "evento": "clientes",
            "creado": "2019-05-21 22:39:27",
            "updated": "2019-05-23 22:26:08",
            "url": "http://urldeejemplo.com.ar/ntf.php"
        },
        {
            "id": 2,
            "evento": "pedidos",
            "creado": "2019-05-21 22:46:44",
            "updated": "2019-05-23 22:26:08",
            "url": "http://urldeejemplo.com.ar/ntf.php"
        },
        {
            "id": 3,
            "evento": "productos",
            "creado": "2019-05-21 04:24:15",
            "updated": "2019-05-23 22:26:08",
            "url": "http://urldeejemplo.com.ar/ntf.php"
        },
        {
            "id": 4,
            "evento": "categorias",
            "creado": "2019-05-21 22:46:44",
            "updated": "2019-05-23 22:26:08",
            "url": "http://urldeejemplo.com.ar/ntf.php"
        },
        {
            "id": 5,
            "evento": "marcas",
            "creado": "2019-05-21 22:46:44",
            "updated": "2019-05-23 22:26:08",
            "url": "http://urldeejemplo.com.ar/ntf.php"
        },
        {
            "id": 6,
            "evento": "listas_precio",
            "creado": "2019-05-21 22:40:56",
            "updated": "2019-05-23 22:26:08",
            "url": "http://urldeejemplo.com.ar/ntf.php"
        },
        {
            "id": 7,
            "evento": "sucursales",
            "creado": "2019-05-21 22:40:56",
            "updated": "2019-05-23 22:26:08",
            "url": "http://urldeejemplo.com.ar/ntf.php"
        },
        {
            "id": 8,
            "evento": "cotizaciones",
            "creado": "2019-05-21 22:46:44",
            "updated": "2019-05-23 22:26:08",
            "url": "http://urldeejemplo.com.ar/ntf.php"
        }
    ]
}
```