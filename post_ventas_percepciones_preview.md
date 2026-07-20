### Descripción:

Resuelve las percepciones automáticas de una venta utilizando la misma lógica funcional que hoy usa la interfaz de ventas. La respuesta devuelve `percepciones[]` listo para reutilizarse en `POST /api/v2/ventas/alta`.

### URL:

`https://cianbox.org/{cuenta}/api/v2/ventas/percepciones/preview`

### Método: POST

### Parámetros:
```json
{
    "fecha": "2026-04-01",
    "id_cliente": 257,
    "id_punto_venta": 1,
    "productos": [
        {
            "id": 95,
            "cantidad": 1,
            "neto_uni": 16211,
            "alicuota": 21
        },
        {
            "id": 0,
            "tipo": "concepto_libre",
            "detalle": "Instalacion",
            "cantidad": 1,
            "neto_uni": 1000,
            "alicuota": 21
        }
    ]
}
```

### Ejemplo:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{
        "fecha": "2026-04-01",
        "id_cliente": 257,
        "id_punto_venta": 1,
        "productos": [
            {
                "id": 95,
                "cantidad": 1,
                "neto_uni": 16211,
                "alicuota": 21
            }
        ]
    }' \
'https://cianbox.org/micuenta/api/v2/ventas/percepciones/preview?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:
```json
{
    "status": "ok",
    "scheme": "http",
    "host": "cianbox.test",
    "account": "micuenta",
    "module": "pv_ventas",
    "method": "POST",
    "body": {
        "status": "ok",
        "percepciones": [
            {
                "id_tipo_percepcion": 18,
                "id_regimen": 0,
                "id_impuesto": 3,
                "base_imponible": 17211,
                "monto": 516.33,
                "alicuota": 3
            }
        ]
    }
}
```

### Uso recomendado:

1. Consultar el preview.
2. Tomar el array `body.percepciones`.
3. Enviarlo sin cambios dentro de `percepciones[]` al endpoint `POST /api/v2/ventas/alta`.

### Notas:

- Si para el cliente/punto de venta no corresponde aplicar percepciones automáticas, la respuesta será `percepciones: []`.
- Este endpoint no crea ventas ni modifica datos comerciales.
