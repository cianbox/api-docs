### Descripción:

Obtiene las Listas de Precio

### URL:

`https://cianbox.org/{cuenta}/api/v2/productos/listas`

o

`https://cianbox.org/{cuenta}/api/v2/productos/listas/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id de/las listas de precio ej. 2 o 1,3,4      |
|page         |NO        |Página solicitada                             |
|limit        |NO        |Límite de ítems por petición                  |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,producto|
|order        |NO        |Ordena el listado, acepta los valores: name-asc, name-desc, id-asc, id-desc|


### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/productos/listas?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
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
        "lista",
        "vencimiento",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 1,
            "lista": "Efectivo, Debito, Credito 1 Pago",
            "vencimiento": null,
            "vigente": true
        },
        {
            "id": 2,
            "lista": "Todo Pago 3 y 6 Pagos",
            "vencimiento": null,
            "vigente": true
        },
        {
            "id": 3,
            "lista": "Plan Ahora 12",
            "vencimiento": null,
            "vigente": true
        },
        {
            "id": 4,
            "lista": "Plan Ahora 18",
            "vencimiento": null,
            "vigente": true
        },
        {
            "id": 5,
            "lista": "Lista Gremio",
            "vencimiento": null,
            "vigente": true
        }
    ]
}
```