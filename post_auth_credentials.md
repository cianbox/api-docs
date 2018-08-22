### Descripción:

Obtiene las credenciales de acceso (token de acceso y refresco) usando usuario y contraseña válidos de Cianbox.

### URL:

`https://cianbox.org/{cuenta}/api/v2/auth/credentials`

### Método: POST

### Parámetros:

|Parámetro |Requerido |Descripción                 |Ejemplo         |
|----------|----------|----------------------------|----------------|
|app_name  |SI        |Nombre de la aplicación     |Mi App re Copada|
|app_code  |SI        |Código de la aplicación     |mi-app-re-copada|
|user      |SI        |Nombre de usuario de Cianbox|                |
|password  |SI        |Contraseña de Cianbox       |                |

### Ejemplo:
```bash
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" \
-d "app_name=Mi App&app_code=mi-app&user=usuario&password=secreto1234" \
'https://cianbox.org/micuenta/api/v2/auth/credentials'
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
        "access_token": "CBX_AT-R8xyfKa0Wi9qeIG5-130033-q2cxQIojoHVQnsXxmiXQinXmJlUEWt1p-570984383",
        "refresh_token": "CBX_RT-8hY8A80WGMiHVKCKFOrXjtMP-734794790-SkAeRIGtEJeQRmhG-446258",
        "expires_in": 85497
    }
}
```
|Valor         |Descripción |
|--------------|------------|
|access_token  |Token de acceso temporal, vence cada 24 horas (tiempo restante determinado por **expires_in**)|
|refresh_token |Token de refresco, sirve para solicitar un nuevo token de acceso. Vence cada 600 días, y una vez vencido hay que repetir el proceso de obtención de credenciales vía usuario y contraseña|
|expires_in    |Tiempo restante del token de acceso expresado en segundos|