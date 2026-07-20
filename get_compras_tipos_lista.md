### Descripción:

Obtiene los tipos/letras disponibles para cargar compras.

### URL:

`https://cianbox.org/{cuenta}/api/v2/compras/tipos`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|access_token|SI|Token de acceso válido|
|id|NO|id del/los tipos|
|fiscal|NO|`true` o `false`|
|vigente|NO|`true`, `false` o `all`. Predeterminado: `true`|
|fields|NO|Campos de `available_fields` separados por coma|

### Ejemplo:

```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/compras/tipos?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:

```json
{
    "status": "ok",
    "module": "pv_compras",
    "method": "GET",
    "body": [
        {
            "id": 1,
            "tipo": "A",
            "fiscal": true,
            "discrimina_iva": true,
            "vigente": true
        }
    ]
}
```
