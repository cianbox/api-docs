### Descripción:

Crea un remito interno de transferencia de stock entre sucursales reutilizando el circuito real del sistema.

### URL:

`https://cianbox.org/{cuenta}/api/v2/stock/remito_interno/alta`

### Método: POST

### Payload base:
```json
{
    "fecha": "2026-04-09",
    "id_sucursal_origen": 1,
    "id_punto_venta": 7,
    "id_sucursal_destino": 3,
    "observaciones": "Transferencia de mercaderia entre sucursales",
    "entregado": false,
    "productos": [
        {
            "id_producto": 265,
            "cantidad": 10
        },
        {
            "id_producto": 761,
            "cantidad": 2,
            "numeros_serie": [
                {
                    "sn": "NS-0001",
                    "aduana": "",
                    "anio": "",
                    "id_pais": 0,
                    "id_uso": 0
                },
                {
                    "sn": "NS-0002",
                    "aduana": "",
                    "anio": "",
                    "id_pais": 0,
                    "id_uso": 0
                }
            ]
        }
    ]
}
```

### Reglas importantes:

- `fecha` es obligatoria y debe tener formato `YYYY-MM-DD`.
- `id_sucursal_origen` es obligatorio.
- `id_punto_venta` es obligatorio y debe corresponder a un talonario interno habilitado para el usuario autenticado.
- `id_sucursal_destino` es obligatoria.
- `id_sucursal_destino` debe ser distinta de `id_sucursal_origen`.
- El número de comprobante siempre se asigna automáticamente.
- `entregado` es obligatorio y acepta `true` o `false`.
- `productos[]` es obligatorio y acepta hasta 200 ítems.
- Cada ítem debe informar `id_producto` y `cantidad`.
- `numeros_serie[]` es opcional y sólo puede enviarse para productos que manejen números de serie.
- La cantidad de números de serie de un ítem nunca puede superar la cantidad del producto.
- Los productos deben estar asociados a la integración API autenticada.
- Si la cuenta no tiene habilitado `forzar_entrega_remito`, el endpoint valida stock disponible en la sucursal de origen antes de ejecutar el alta.
- El alta mantiene la misma lógica del sistema para imputación PEPS/UEPS, números de serie y datos de despacho/importación.

### Respuesta exitosa:
```json
{
    "status": "ok",
    "description": "El remito interno se cargó correctamente",
    "id": 12345
}
```

### Casos de uso

#### 1. Remito interno pendiente de recibir
```json
{
    "fecha": "2026-04-09",
    "id_sucursal_origen": 1,
    "id_punto_venta": 7,
    "id_sucursal_destino": 3,
    "observaciones": "Envio a deposito central",
    "entregado": false,
    "productos": [
        { "id_producto": 265, "cantidad": 10 }
    ]
}
```

#### 2. Remito interno entregado al momento del alta
```json
{
    "fecha": "2026-04-09",
    "id_sucursal_origen": 1,
    "id_punto_venta": 7,
    "id_sucursal_destino": 3,
    "entregado": true,
    "productos": [
        { "id_producto": 761, "cantidad": 2 }
    ]
}
```
