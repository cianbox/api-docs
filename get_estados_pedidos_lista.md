### Descripción:

Obtiene un estado o lista de estados de pedidos

### URL:

`https://cianbox.org/{cuenta}/api/v2/pedidos/estados`

o

`https://cianbox.org/{cuenta}/api/v2/pedidos/estados/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id del/los estados ej. 5 o 2,4,7              |
|page         |NO        |Página solicitada                             |
|limit        |NO        |Límite de ítems por petición                  |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,producto|
|order        |NO        |Ordena el listado, acepta los valores: name-asc, name-desc, id-asc, id-desc|


### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/pedidos/estados?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_pedidos",
    "method": "GET",
    "available_fields": [
        "id",
        "estado",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 1,
            "estado": "Reservado",
            "vigente": true
        },
        {
            "id": 2,
            "estado": "En Preparación",
            "vigente": true
        },
        {
            "id": 3,
            "estado": "Listo para Facturar",
            "vigente": true
        }
    ]
}
```