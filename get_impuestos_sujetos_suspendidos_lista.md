### Descripción:

Lista sujetos suspendidos AFIP para completar `id_ss` en retenciones de pagos/cobros.

### URL:

`https://cianbox.org/{cuenta}/api/v2/impuestos/sujetos_suspendidos`

### Método: GET

### Parámetros:

|Parámetro|Requerido|Descripción|
|---|---|---|
|id|NO|Uno o varios IDs separados por coma|
|codigo|NO|Código AFIP|
|search|NO|Busca por descripción o código|
|fields|NO|Campos a devolver|
|order|NO|`code-asc`, `code-desc`, `name-asc`, `name-desc`, `id-asc`, `id-desc`|
|page|NO|Página|
|limit|NO|Cantidad por página, máximo 200|

### Ejemplo:

```bash
curl 'https://cianbox.org/micuenta/api/v2/impuestos/sujetos_suspendidos?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:

```json
{
    "status": "ok",
    "body": [
        {
            "id": 1,
            "codigo": 0,
            "segun": "Ninguno",
            "descripcion": "0 - Ninguno"
        }
    ]
}
```
