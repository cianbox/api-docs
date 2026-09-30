### Descripción:

Obtiene los contribuyentes disponibles para cargar compras.

El registro con `id = 0` representa el contribuyente principal configurado en la cuenta.

### URL:

`https://cianbox.org/{cuenta}/api/v2/compras/contribuyentes`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|access_token|SI|Token de acceso válido|
|id|NO|Filtra por uno o más IDs. Puede usarse `0` para el contribuyente principal|
|cuit|NO|Busca por CUIT, con o sin guiones|
|search|NO|Busca por razón social, nombre o CUIT|
|vigente|NO|`true`, `false` o `all`. Predeterminado: `true`|
|page|NO|Página solicitada|
|limit|NO|Límite de ítems por petición. Máximo: 200|
|fields|NO|Campos de `available_fields` separados por coma|
|order|NO|Acepta `name-asc`, `name-desc`, `id-asc`, `id-desc`|

### Ejemplo:

```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/compras/contribuyentes?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&fields=id,razon,cuit,predeterminado'
```

### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_compras",
    "method": "GET",
    "available_fields": [
        "id",
        "razon",
        "cuit",
        "id_condicion",
        "condicion",
        "principal",
        "predeterminado",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 0,
            "razon": "Empresa Demo SA",
            "cuit": "30700000001",
            "predeterminado": true
        }
    ]
}
```

### Uso en alta de compras:

Enviar el valor en `id_contribuyente`:

```json
{
    "id_contribuyente": 0
}
```

También puede enviarse `cuit_contribuyente`; el endpoint de alta lo resuelve contra el contribuyente principal o contra `lista_contribuyentes`.
