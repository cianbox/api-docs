### Descripción:

Obtiene una marca o lista de marcas

### URL:

`https://cianbox.org/{cuenta}/api/v2/productos/marcas`

o

`https://cianbox.org/{cuenta}/api/v2/productos/marcas/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id del/las marcas ej. 15 o 33,17,19           |
|page         |NO        |Página solicitada                             |
|limit        |NO        |Límite de ítems por petición                  |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,producto|
|order        |NO        |Ordena el listado, acepta los valores: name-asc, name-desc, id-asc, id-desc|


### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/productos/marcas?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_productos",
    "method": "GET",
    "available_fields": [
        "id",
        "marca",
        "vigente"
    ],
    "page": 1,
    "total_pages": 143,
    "body": [
        {
            "id": 1,
            "marca": "NOGA NET",
            "vigente": true
        },
        {
            "id": 2,
            "marca": "NIMARK",
            "vigente": true
        },
        {
            "id": 3,
            "marca": "GENIUS",
            "vigente": true
        }
    ]
}
```