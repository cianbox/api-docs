### Descripción:

Obtiene bienes de uso disponibles para usar en el alta de compras.

En `POST /api/v2/compras/alta`, los bienes de uso se envían dentro de `productos[]` con `tipo = "bien_uso"`. Si se informa `id`, debe existir en `tabla_bienes_uso`; si no se informa, el proceso legacy crea o reutiliza el bien por `detalle` e `id_tipo_bien_uso`.

### URL:

`https://cianbox.org/{cuenta}/api/v2/compras/bienes_uso`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|access_token|SI|Token de acceso válido|
|id|NO|Filtra por uno o más bienes de uso|
|id_tipo_bien_uso|NO|Filtra por uno o más tipos de bien de uso|
|id_contribuyente|NO|Filtra por contribuyente fiscal. `0` representa el contribuyente principal|
|search|NO|Busca por descripción del bien o tipo de bien|
|vigente|NO|`true`, `false` o `all`. Predeterminado: `true`|
|page|NO|Página solicitada|
|limit|NO|Límite de ítems por petición. Máximo: 200|
|fields|NO|Campos de `available_fields` separados por coma|
|order|NO|Acepta `name-asc`, `name-desc`, `id-asc`, `id-desc`|

### Ejemplo:

```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/compras/bienes_uso?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&fields=id,descripcion,id_tipo_bien_uso,tipo_bien_uso'
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
        "id_tipo_bien_uso",
        "tipo_bien_uso",
        "cantidad",
        "vida_util",
        "fecha_alta",
        "fecha_baja",
        "valor_origen",
        "amortizacion_anual",
        "id_tipo_amortizacion",
        "id_contribuyente",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 8,
            "descripcion": "Silla Gamer",
            "id_tipo_bien_uso": 2,
            "tipo_bien_uso": "Muebles y útiles",
            "vigente": true
        }
    ]
}
```

### Uso en alta de compras:

```json
{
    "tipo": "bien_uso",
    "id": 8,
    "cantidad": 1,
    "neto_uni": 1200,
    "alicuota": 21
}
```

Para alta automática, `id_tipo_bien_uso` es obligatorio:

```json
{
    "tipo": "bien_uso",
    "detalle": "Notebook para administración",
    "id_tipo_bien_uso": 2,
    "cantidad": 1,
    "neto_uni": 1200,
    "alicuota": 21
}
```
