### Descripción:

Obtiene un cliente o lista de clientes

### URL:

`https://cianbox.org/{cuenta}/api/v2/clientes`

o

`https://cianbox.org/{cuenta}/api/v2/clientes/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id del/los clientes ej. 1566 o 143,188,19     |
|page         |NO        |Página solicitada                             |
|limit        |NO        |Límite de ítems por petición                  |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,razon|
|order        |NO        |Ordena el listado, acepta los valores: create-date-asc, create-date-desc, modified-date-asc, modified-date-desc, id-asc, id-desc|


### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/clientes?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
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
        "updated",
        "razon",
        "condicion",
        "tipo_documento",
        "numero_documento",
        "domicilio",
        "localidad",
        "provincia",
        "telefono",
        "celular",
        "email",
        "ctacte",
        "plazo",
        "limite",
        "saldo",
        "descuento",
        "observaciones",
        "usuarios"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 17,
            "updated": "2018-09-17 13:05:25",
            "razon": "Juan Ignacio Innomindado",
            "condicion": "RI",
            "tipo_documento": "CUIT",
            "numero_documento": "30999999991",
            "domicilio": "San Martín 1234",
            "localidad": "Santa Rosa de Calamuchita",
            "provincia": "Córdoba",
            "telefono": "3546555555",
            "celular": "3546888888",
            "email": "juanignacio@mail.com.ar",
            "ctacte": true,
            "plazo": 30,
            "limite": 45000,
            "saldo": 23781.32,
            "descuento": 0,
            "observaciones": "Abono hasta octubre 2018 $2805"
        }
    ]
}
```