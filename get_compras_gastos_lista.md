### Descripción:

Obtiene gastos disponibles para usar en el alta de compras.

En `POST /api/v2/compras/alta`, los gastos se envían dentro de `productos[]` con `tipo = "gasto"`. Si se informa `id`, debe existir en `tabla_gastos`; si no se informa, el proceso legacy crea o reutiliza el gasto por descripción.

### URL:

`https://cianbox.org/{cuenta}/api/v2/compras/gastos`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|access_token|SI|Token de acceso válido|
|id|NO|Filtra por uno o más gastos|
|search|NO|Busca por descripción|
|vigente|NO|`true`, `false` o `all`. Predeterminado: `true`|
|page|NO|Página solicitada|
|limit|NO|Límite de ítems por petición. Máximo: 200|
|fields|NO|Campos de `available_fields` separados por coma|
|order|NO|Acepta `name-asc`, `name-desc`, `id-asc`, `id-desc`|

### Ejemplo:

```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/compras/gastos?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&search=alquiler&fields=id,descripcion'
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
        "descripcion",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 8632,
            "descripcion": "Alquiler local",
            "vigente": true
        }
    ]
}
```

### Uso en alta de compras:

```json
{
    "tipo": "gasto",
    "id": 8632,
    "cantidad": 1,
    "neto_uni": 780,
    "alicuota": 21
}
```

Para alta automática:

```json
{
    "tipo": "gasto",
    "detalle": "Gasto creado por API",
    "cantidad": 1,
    "neto_uni": 780,
    "alicuota": 21
}
```
