### Descripción:

Crea un nuevo cliente

### URL:

`https://cianbox.org/{cuenta}/api/v2/clientes/alta`

### Método: POST

### Parámetros:
```json
{
    "razon": "Pedro García",
    "condicion": "MT|RI|EXE|CF|RNI|NR|CE",
    "tipo_documento": "CUIT|CUIL|DNI|LE|LC|Pasaporte|CI Extranjera",
    "numero_documento": "20999999994",
    "telefono": "+54 343 12345656",
    "celular": "+54 343 123558877",
    "email": "pedrogarcia@mail.com.ar",
    "domicilio": "Av. Ramirez 1234",
    "localidad": "Paraná",
    "provincia": "Entre Ríos",
    "codigo_postal": 3116,
    "observaciones": "Observaciones sobre el cliente",
    "id_categoria": 3,
    "ids_listas_precio": [0,1,5]
}
```

### Ejemplo:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{ \
        "razon": "Pedro García", \
        "condicion": "MT", \
        "tipo_documento": "CUIT", \
        "numero_documento": "20999999994", \
        "telefono": "+54 343 12345656", \
        "celular": "+54 343 123558877", \
        "email": "pedrogarcia@mail.com.ar", \
        "domicilio": "Av. Ramirez 1234", \
        "localidad": "Paraná", \
        "provincia": "Entre Ríos", \
        "codigo_postal": 3116, \
        "observaciones": "Observaciones sobre el cliente", \
        "id_categoria": 3, \
        "ids_listas_precio": [0,1,5] \
    }' \
'https://cianbox.org/micuenta/api/v2/clientes/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```
### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_clientes",
    "method": "POST",
    "body": {
        "status": "ok",
        "description": "El cliente Pedro García (1581) se cargó correctamente",
        "id": 1581
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
|id            |ID del cliente|
