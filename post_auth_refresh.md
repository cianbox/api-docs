### Descripción:

Obtiene un nuevo token de acceso usando un token de refresco válido.

### URL:

`https://cianbox.org/{cuenta}/api/v2/auth/refresh`

### Método: POST

### Parámetros:

|Parámetro    |Requerido |Descripción              |
|-------------|----------|-------------------------|
|refresh_token|SI        |Token de refresco válido |


### Ejemplos:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"refresh_token":"CBX_RT-czntKqNbP87PLT6ai2c0mDle-289145332-3ONbLx2q4o9AtkZu-559849"}' \
'https://cianbox.org/micuenta/api/v2/auth/refresh'
```
```bash
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" \
-d "refresh_token=CBX_RT-czntKqNbP87PLT6ai2c0mDle-289145332-3ONbLx2q4o9AtkZu-559849" \
'https://cianbox.org/micuenta/api/v2/auth/refresh'
```
### Respuesta:
```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "auth",
    "method": "POST",
    "body": {
        "access_token": "CBX_AT-c2pGCQqkR8QefYGw-947800-R6Rq8NwqvrCHuk9zmoddW49bDbhrMGqD-311038496",
        "expires_in": 86107
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|access_token  |Token de acceso temporal, vence cada 24 horas (tiempo restante determinado por **expires_in**)|
|expires_in    |Tiempo restante del token de acceso expresado en segundos|