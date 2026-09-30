### Descripción:

Recursos auxiliares de caja para preparar pagos por API v2. Se usan principalmente desde `POST /api/v2/compras/alta` cuando `forma_pago` es `contado_mixto`.

### Autenticación:

Todos los endpoints usan el mismo `access_token` del resto de la API v2.

### Endpoints disponibles:

|Endpoint|Uso|
|---|---|
|`GET /api/v2/caja/cuentas_bancarias`|Consulta cuentas bancarias para crear transferencias en una orden de pago|
|`GET /api/v2/caja/transferencias_pendientes`|Consulta transferencias bancarias innominadas pendientes de imputar|
|`GET /api/v2/caja/valores`|Consulta valores/cheques disponibles para informar `pago.valores[].id_valor`|
|`GET /api/v2/caja/chequeras`|Consulta chequeras abiertas y próximo número disponible|
|`POST /api/v2/caja/valores/alta`|Emite un cheque propio y devuelve `id_valor`|
|`GET /api/v2/caja/tipos_retencion`|Consulta tipos de retención y próximo número sugerido|
|`GET /api/v2/impuestos/regimenes`|Consulta regímenes impositivos; admite `id_tipo_retencion`|
|`GET /api/v2/impuestos/sujetos_suspendidos`|Consulta sujetos suspendidos AFIP para completar `id_ss`|

### Ejemplos:

#### Cuentas bancarias
```bash
curl 'https://cianbox.org/micuenta/api/v2/caja/cuentas_bancarias?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_moneda=1'
```

#### Transferencias pendientes
```bash
curl 'https://cianbox.org/micuenta/api/v2/caja/transferencias_pendientes?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_moneda=1'
```

#### Valores disponibles
```bash
curl 'https://cianbox.org/micuenta/api/v2/caja/valores?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&origen=propio&fields=id,numero_formateado,entidad,monto,fecha_vencimiento'
```

#### Chequeras abiertas
```bash
curl 'https://cianbox.org/micuenta/api/v2/caja/chequeras?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_moneda=1&fields=id,descripcion,proximo_numero'
```

#### Emitir cheque propio
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"id_chequera":1,"fecha_cheque":"2026-07-02","fecha_vencimiento":"2026-07-10","monto":1500,"destinatario":"Proveedor de prueba","no_a_la_orden":false,"cruzado":false}' \
'https://cianbox.org/micuenta/api/v2/caja/valores/alta?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

#### Tipos de retención
```bash
curl 'https://cianbox.org/micuenta/api/v2/caja/tipos_retencion?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_punto_venta_pago=9'
```

#### Regímenes de una retención
```bash
curl 'https://cianbox.org/micuenta/api/v2/impuestos/regimenes?access_token=CBX_AT-TcIHdWOvdpIMNsXG...&id_tipo_retencion=1'
```

#### Sujetos suspendidos
```bash
curl 'https://cianbox.org/micuenta/api/v2/impuestos/sujetos_suspendidos?access_token=CBX_AT-TcIHdWOvdpIMNsXG...'
```

### Notas:

- `caja/valores` lista por defecto valores vigentes, disponibles, no anulados, no rechazados y asociados a la caja del usuario de la API.
- `caja/chequeras` devuelve `proximo_numero` para chequeras físicas. Para e-cheques, el número debe informarse manualmente en el alta del valor.
- `caja/tipos_retencion` devuelve `punto_venta` y `proximo_numero`, equivalentes a los valores sugeridos por la pantalla de orden de pago.
- Para usar un cheque propio en una compra con `contado_mixto`, primero emitirlo con `POST /api/v2/caja/valores/alta` y luego enviar el `id_valor` devuelto dentro de `pago.valores[]`.
