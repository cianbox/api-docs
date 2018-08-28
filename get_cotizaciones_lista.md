### Descripción:

Obtiene las Divisas y Cotizaciones

### URL:

`https://cianbox.org/{cuenta}/api/v2/general/cotizaciones`

o

`https://cianbox.org/{cuenta}/api/v2/general/cotizaciones/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id de/las monedas ej. 2 o 1,3,4               |
|page         |NO        |Página solicitada                             |
|limit        |NO        |Límite de ítems por petición                  |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,producto|
|order        |NO        |Ordena el listado, acepta los valores: name-asc, name-desc, id-asc, id-desc|


### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/general/cotizaciones?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
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
    "available_fields": [
        "id",
        "moneda",
        "simbolo",
        "codigo_afip",
        "cotizacion",
        "principal",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 1,
            "moneda": "Peso",
            "simbolo": "$",
            "codigo_afip": "PES",
            "cotizacion": 1,
            "principal": true,
            "vigente": true
        },
        {
            "id": 2,
            "moneda": "Dólar",
            "simbolo": "u$s",
            "codigo_afip": "DOL",
            "cotizacion": 31.9,
            "principal": false,
            "vigente": true
        },
        {
            "id": 3,
            "moneda": "Euro",
            "simbolo": "€",
            "codigo_afip": "060",
            "cotizacion": 38.6,
            "principal": false,
            "vigente": false
        }
    ]
}
```