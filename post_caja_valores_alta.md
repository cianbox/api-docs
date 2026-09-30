### Descripción:

Emite un cheque propio reutilizando la lógica del alta de valor de `pv_caja`. La respuesta devuelve `id_valor`, que luego puede enviarse en `pago.valores[]` de `POST /api/v2/compras/alta`.

### URL:

`https://cianbox.org/{cuenta}/api/v2/caja/valores/alta`

### Método: POST

### Payload:

```json
{
    "id_chequera": 1,
    "fecha_cheque": "2026-07-02",
    "fecha_vencimiento": "2026-07-10",
    "numero": 123456,
    "monto": 1500,
    "destinatario": "Proveedor de prueba",
    "no_a_la_orden": false,
    "cruzado": false
}
```

### Campos:

|Campo|Requerido|Descripción|
|---|---|---|
|id_chequera|SI|Chequera abierta. Consultar con `GET /api/v2/caja/chequeras`|
|fecha_cheque|NO|Fecha de emisión, formato `YYYY-MM-DD`. Si se omite usa la fecha actual|
|fecha_vencimiento|SI|Fecha de cobro, formato `YYYY-MM-DD`|
|numero|NO|Número del cheque. En chequeras físicas puede omitirse y se usa el próximo disponible. En e-cheques es obligatorio|
|monto|SI|Monto del valor|
|destinatario|NO|Destinatario del cheque|
|no_a_la_orden|NO|Marca el cheque como no a la orden|
|cruzado|NO|Marca el cheque como cruzado|

### Ejemplo:

```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"id_chequera":1,"fecha_cheque":"2026-07-02","fecha_vencimiento":"2026-07-10","monto":1500,"destinatario":"Proveedor de prueba"}' \
'https://cianbox.org/micuenta/api/v2/caja/valores/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:

```json
{
    "status": "ok",
    "description": "El valor [Banco Ejemplo :: Nro 00123456] se cargo correctamente",
    "id": 1570,
    "id_valor": 1570,
    "values": {
        "id_valor": 1570
    },
    "numero": "123456",
    "numero_formateado": "00123456",
    "monto": 1500
}
```

### Uso en compras:

```json
{
    "pago": {
        "valores": [
            {
                "id_valor": 1570
            }
        ]
    }
}
```
