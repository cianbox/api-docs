### Descripción:

Crea un nuevo proveedor reutilizando el circuito real de `modules/pv_proveedores/alta_proc.php`.

### URL:

`https://cianbox.org/{cuenta}/api/v2/proveedores/alta`

### Método: POST

### Payload base:

```json
{
    "razon": "Proveedor Demo SRL",
    "condicion": "RI",
    "tipo_documento": "CUIT",
    "numero_documento": "30700000001",
    "nombre": "Proveedor Demo",
    "numero_iibb": "123456789",
    "domicilio": "Av. Ejemplo 1234",
    "id_localidad": 1,
    "telefono": "+54 343 1234567",
    "celular": "+54 343 155555555",
    "email": "compras@proveedordemo.com",
    "cta_cte": true,
    "plazo": 30,
    "monto": 100000,
    "id_cuenta": 0,
    "id_credito_fiscal": 0,
    "id_categoria_compra": 0,
    "observaciones": "Proveedor creado por API",
    "actualiza_costos": true,
    "prorratea_iva": true
}
```

### Campos principales:

|Campo|Requerido|Descripción|
|---|---|---|
|razon|SI|Apellido y nombre o razón social del proveedor|
|condicion|NO|Acepta `MT`, `RI`, `EXE`, `CF`, `RNI`, `NR`, `CE`. También puede enviarse un `id_condicion` vigente|
|tipo_documento|NO|Acepta `CUIT`, `CUIL`, `DNI`, `LE`, `LC`, `Pasaporte`, `CI Extranjera`. También puede enviarse un `id_tipo_documento` vigente|
|numero_documento|NO|CUIT/documento del proveedor. Alias: `cuit`|
|nif|NO|NIF del proveedor|
|nombre|NO|Nombre de fantasía|
|numero_iibb|NO|Inscripción IIBB|
|domicilio|NO|Domicilio del proveedor|
|id_localidad|NO|Localidad vigente existente en Cianbox|
|id_sucursal|NO|Sucursal vigente asociada, si la cuenta separa proveedores por sucursal|
|telefono|NO|Teléfono principal|
|celular|NO|Celular|
|email|NO|Correo principal. Alias: `mail`|
|web|NO|Sitio web|
|contacto|NO|Contacto principal|
|cta_cte|NO|Habilita cuenta corriente. Predeterminado: `false`|
|plazo|NO|Plazo en días para cuenta corriente|
|monto|NO|Monto máximo de cuenta corriente|
|id_cuenta|NO|Cuenta contable vigente e imputable|
|id_credito_fiscal|NO|Concepto fiscal de compras vigente|
|id_categoria_compra|NO|Categoría de compra vigente|
|id_estado|NO|Estado vigente del proveedor|
|actualiza_costos|NO|Indica si actualiza costos al cargar compras. Predeterminado: `true`|
|cuenta_orden|NO|Marca al proveedor como cuenta y orden. Predeterminado: `false`|
|prorratea_iva|NO|Indica si prorratea IVA. Predeterminado: `true`|
|id_condicion_sicore|NO|Condición SICORE existente. Alias: `condicion_sicore`|
|inscripto_cm|NO|Marca inscripción en convenio multilateral|
|id_tipo_operacion_ater|NO|Tipo de operación ATER vigente y habilitado para retenciones|
|observaciones|NO|Observaciones internas|

### Contactos:

```json
{
    "contactos": [
        {
            "nombre": "Area Comercial",
            "telefono1": "+54 343 1234567",
            "telefono2": "",
            "email": "ventas@proveedordemo.com"
        }
    ]
}
```

### Cuentas bancarias:

```json
{
    "cuentas_bancarias": [
        {
            "id_entidad": 1,
            "numero_sucursal": "001",
            "numero_cuenta": "123456",
            "cbu": "0000000000000000000000"
        }
    ]
}
```

`id_entidad` debe existir y estar vigente en la lista de entidades bancarias de la cuenta. Todos los IDs de referencia informados se validan antes de crear el proveedor.

### Ejemplo:

```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"razon":"Proveedor Demo SRL","condicion":"RI","tipo_documento":"CUIT","numero_documento":"30700000001","email":"compras@proveedordemo.com","cta_cte":true,"plazo":30}' \
'https://cianbox.org/micuenta/api/v2/proveedores/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Respuesta:

```json
{
    "status": "ok",
    "scheme": "https",
    "host": "cianbox.org",
    "account": "micuenta",
    "module": "pv_proveedores",
    "method": "POST",
    "body": {
        "status": "ok",
        "description": "El proveedor Proveedor Demo SRL (27) se cargó correctamente",
        "id": 27
    }
}
```

### Webhooks

El recurso dispone del evento `proveedores`, cuyo `endpoint` es `proveedores`.

Se genera una notificación cuando:

- se carga un proveedor desde la interfaz o desde `POST /api/v2/proveedores/alta`;
- se modifican sus datos, su vigencia o la configuración de prorrateo de IVA;
- se insertan o actualizan proveedores mediante la importación masiva;
- se unifican proveedores. En este caso se informan el ID conservado y el ID dado de baja.

El webhook se configura con `POST /api/v2/general/notificaciones/alta`:

```json
{
    "evento": ["proveedores"],
    "url": "https://integracion.ejemplo.com/webhooks/cianbox"
}
```

Ejemplo del cuerpo enviado a la URL configurada:

```json
{
    "event": "proveedores",
    "created": "2026-07-20 14:30:00",
    "id": ["27"],
    "endpoint": "proveedores"
}
```

`id` siempre es un arreglo y puede incluir más de un proveedor. Para obtener el estado actualizado se debe consultar `GET /api/v2/proveedores?id=27`. Si fue dado de baja, se debe usar `GET /api/v2/proveedores?id=27&vigente=all`.
