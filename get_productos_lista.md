### Descripción:

Obtiene un producto o lista de productos

### URL:

`https://cianbox.org/{cuenta}/api/v2/productos`

o

`https://cianbox.org/{cuenta}/api/v2/productos/lista`

### Método: GET

### Parámetros:

|Parámetro    |Requerido |Descripción                                   |
|-------------|----------|----------------------------------------------|
|access_token |SI        |Token de acceso válido                        |
|id           |NO        |id del/los productos ej. 1566 o 1433,1788,19  |
|page         |NO        |Página solicitada                             |
|limit        |NO        |Límite de ítems por petición                  |
|fields       |NO        |Cualquiera de los listados en **available_fields** separados por comas, valor predeterminado: todos los campos. ej. &fields=id,updated,producto|


### Ejemplo:
```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/productos?access_token=CBX_AT-TcIHdWOvdpIMNsXG-485517-hRG87XCcRnpCzhWOHAs1up6KPQykiuvc-663053443'
```
### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_productos",
    "method": "GET",
    "available_fields": [
        "id",
        "updated",
        "producto",
        "id_marca",
        "marca",
        "id_categoria",
        "categoria",
        "descripcion",
        "precio_actualizado",
        "codigo_interno",
        "codigo_barras",
        "costo",
        "stock_total",
        "stock_sucursal",
        "reservado",
        "cantidad_minima",
        "cantidad_critica",
        "precio_neto",
        "precio_oferta",
        "oferta",
        "alicuota_iva",
        "ubicacion",
        "talle",
        "color",
        "genero",
        "temporada",
        "imagenes",
        "vigente"
    ],
    "page": 1,
    "total_pages": 1,
    "body": [
        {
            "id": 17533,
            "updated": "2018-08-02 22:06:19",
            "producto": "DVD BULK X50 IMPRIMIBLE TELTRON -R 16X",
            "id_marca": 70,
            "marca": "TELTRON",
            "id_categoria": 15,
            "categoria": "CD/DVD/CASE",
            "descripcion": "Descripción del producto",
            "precio_actualizado": "2018-05-20",
            "codigo_interno": "DVD-00001",
            "codigo_barras": "9876546543553",
            "costo": 8.456,
            "stock_total": 50,
            "stock_sucursal": [
                {
                    "id_sucursal": 1,
                    "stock": 30
                },
                {
                    "id_sucursal": 2,
                    "stock": 20
                }
            ],
            "reservado": 0,
            "cantidad_minima": 0,
            "cantidad_critica": 0,
            "precio_neto": 12.2612,
            "precio_oferta": 0,
            "oferta": false,
            "alicuota_iva": 1.21,
            "ubicacion": "",
            "talle": "",
            "color": "",
            "genero": null,
            "temporada": "",
            "imagenes": [
                "https://cianbox.org/micuenta/uploads/pv_productos/2018/08/1534977203f036a7ff4bbf5fa28c5a74f382ae61fa.jpg",
                "https://cianbox.org/micuenta/uploads/pv_productos/2018/08/1534977362a807ca81acdd483d2dcd9247a54db4f6.png"
            ],
            "vigente": true
        }
    ]
}
```