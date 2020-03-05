### Descripción:

Editar un cliente

### URL:

`https://cianbox.org/{cuenta}/api/v2/clientes/editar`

### Método: PUT

### Parámetros:

#### vía URL
|Parámetro    |Requerido |Descripción             |
|-------------|----------|------------------------|
|access_token |SI        |Token de acceso válido  |
|id           |SI        |id del cliente a editar |

#### vía JSON
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
    "observaciones": "Observaciones sobre el cliente"
}
```

### Ejemplo:
```shell
curl -X PUT -H "Content-Type: application/json" \
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
        "observaciones": "Observaciones sobre el cliente" \
    }' \
'https://cianbox.org/micuenta/api/v2/clientes/editar?id=713&access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "rpdigital",
    "module": "pv_clientes",
    "method": "PUT",
    "body": {
        "status": "ok",
        "description": "El cliente Pedro García (713) se actualizó correctamente",
        "id": 713
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|status        |Estado de la petición: **ok** o **error**|
|descripcion   |Descripción de la petición|
|id            |ID del cliente actualizado|