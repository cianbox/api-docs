### Descripción:

Obtiene un proveedor o lista de proveedores.

### URL:

`https://cianbox.org/{cuenta}/api/v2/proveedores`

o

`https://cianbox.org/{cuenta}/api/v2/proveedores/lista`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|access_token|SI|Token de acceso válido|
|id|NO|id del/los proveedores, por ejemplo `12` o `12,18,21`|
|numero_documento|NO|CUIT/documento del proveedor|
|nif|NO|NIF del proveedor|
|id_categoria_compra|NO|Filtra por una o más categorías de compra|
|id_estado|NO|Filtra por uno o más estados|
|id_sucursal|NO|Filtra por una o más sucursales|
|vigente|NO|`true`, `false` o `all`. Predeterminado: `true`|
|filter|NO|Busca por razón, nombre, documento, email o código interno|
|page|NO|Página solicitada|
|limit|NO|Límite de ítems por petición. Máximo: 200|
|fields|NO|Campos de `available_fields` separados por coma|
|order|NO|Acepta `create-date-asc`, `create-date-desc`, `id-asc`, `id-desc`, `name-asc`, `name-desc`, `balance-asc`, `balance-desc`|

### Ejemplo:

```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/proveedores?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&fields=id,razon,numero_documento,ctacte,plazo,id_cuenta,id_credito_fiscal,id_categoria_compra,actualiza_costos,prorratea_iva'
```

### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_proveedores",
    "method": "GET",
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 12,
            "razon": "Proveedor SRL",
            "numero_documento": "30700000001",
            "ctacte": true,
            "plazo": 30,
            "id_cuenta": 125,
            "id_credito_fiscal": 1,
            "id_categoria_compra": 4,
            "actualiza_costos": true,
            "prorratea_iva": true
        }
    ]
}
```
