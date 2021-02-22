### Descripción:

Obtiene una categoría de cliente o lista de categorías de cliente

### URL:

`https://cianbox.org/{cuenta}/api/v2/clientes/categorias`

o

`https://cianbox.org/{cuenta}/api/v2/clientes/categorias/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id del/las categorias de cliente ej. 15 o 33,17,19           |
|page         |NO        |Página solicitada                             |
|limit        |NO        |Límite de ítems por petición                  |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,marca,vigente|
|order        |NO        |Ordena el listado, acepta los valores: name-asc, name-desc, id-asc, id-desc|


### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/clientes/categorias?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_clientes",
    "method": "GET",
    "available_fields": [
        "id",
        "categoria",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 1,
            "categoria": "FERRETERIA",
            "vigente": true
        },
        {
            "id": 2,
            "categoria": "ELECTRONICA",
            "vigente": true
        },
        {
            "id": 3,
            "categoria": "BAZAR",
            "vigente": true
        }
    ]
}
```