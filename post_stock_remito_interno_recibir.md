### Descripción:

Recibe un remito interno pendiente, ingresando el stock en la sucursal destino mediante el mismo circuito del sistema.

### URL:

`https://cianbox.org/{cuenta}/api/v2/stock/remito_interno/recibir`

### Método: POST

### Payload base:
```json
{
    "id": 12345
}
```

### Reglas importantes:

- `id` es obligatorio. También se acepta `id_remito` por compatibilidad.
- El remito interno debe existir y encontrarse vigente.
- El remito interno no debe haber sido recibido previamente.
- La recepción reutiliza la misma lógica del sistema para ingreso de stock, traspaso de números de serie y conservación de datos de despacho/importación.

### Respuesta exitosa:
```json
{
    "status": "ok",
    "description": "El remito interno se ingresó correctamente",
    "id": 12345
}
```

### Ejemplo:
```json
{
    "id": 12345
}
```
