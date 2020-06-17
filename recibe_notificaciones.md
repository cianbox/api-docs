## Recibe notificaciones

Para que tu aplicación pueda conocer los eventos que se producen del lado de Cianbox&reg; y actuar en consecuencia,
podés suscribir una o varias URLs (webhooks) a nuestro sistema de notificaciones.

Disponemos de una variedad de eventos que disparan notificaciones en tiempo real cuando se realizan diferentes acciones
dentro de Cianbox&reg;. Por ej. cuando el usuario cambia el precio de un producto, se modifican los datos de un cliente
o se da de baja un pedido.

Con los siguientes recursos podés manejar tus suscripciones:

1. [Listar eventos y webhooks](https://github.com/cianbox/api-docs/blob/master/get_webhook_lista.md)
2. [Asignar un webhook a eventos](https://github.com/cianbox/api-docs/blob/master/post_webhook_alta.md)
3. [Dar de baja un webhook](https://github.com/cianbox/api-docs/blob/master/delete_webhook_eliminar.md)

Una vez suscripto vas a recibir el siguiente JSON en tu/s URL/s:

```json
{
    "event":"productos",
    "created":"2019-05-24 10:58:44",
    "id":[
        "10564", "10725", "587", "964"
    ],
    "endpoint":"productos"
}
```

Cada evento puede notificar hasta 200 ids por cada petición. Así mismo los recursos GET tambien permiten hasta 200 ids
por cada petición, facilitando así la sincronización de los datos.

Por ejempo con los datos de arriba podemos hacer la siguiente petición:

```bash
curl -X GET 'https://cianbox.org/micuenta/api/v2/productos?id=10564,10725,587,964&access_token=CBX_AT-TcIHdWOvdpIMx...'
```

#### Consideraciones

+ Para que la entrega de la notificación se considere exitosa, tu aplicación deberá devolver un estado HTTP 200.
+ Tu aplicación debe responder antes de los 30 segundos, de lo contrario se considerará la notificación como fallida.

#### Eventos

Los eventos a los cuales podés suscribir tus URLs son:

|Evento          |Recurso                                                  |
|----------------|---------------------------------------------------------|
|clientes        |https://cianbox.org/micuenta/api/v2/clientes             |
|pedidos         |https://cianbox.org/micuenta/api/v2/pedidos              |
|productos       |https://cianbox.org/micuenta/api/v2/productos            |
|categorias      |https://cianbox.org/micuenta/api/v2/productos/categorias |
|marcas          |https://cianbox.org/micuenta/api/v2/productos/marcas     |
|listas_precio   |https://cianbox.org/micuenta/api/v2/productos/listas     |
|sucursales      |https://cianbox.org/micuenta/api/v2/productos/sucursales |
|cotizaciones    |https://cianbox.org/micuenta/api/v2/general/cotizaciones |
|estados         |https://cianbox.org/micuenta/api/v2/pedidos/estados      |

#### Código de ejemplo

```php
<?php
header("Access-Control-Allow-Orgin: *");
header("Access-Control-Allow-Methods: *");
header('Content-Type: application/json; charset=UTF-8');
header("HTTP/1.1 200 OK");

$data = json_decode(file_get_contents("php://input"), TRUE);

$evento = $data['event'];
$ids    = $data['id'];
/*
 * Acá va el código de tu aplicación para realizar la petición a la API
 */
?>
```