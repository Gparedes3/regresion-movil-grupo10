# Suite de regresión · MercaMóvil (bug #482)

Cambio: `recalcularTotal()`. Lo usan el carrito, el resumen de pago y los cupones; `CarritoRepository` persiste el total calculado.

| Caso | Descripción | Clasificación |
|---|---|---|
| C01 | Iniciar sesión con credenciales válidas | Smoke |
| C02 | Abrir el catálogo y ver la lista de productos | Smoke |
| C03 | Completar una compra de punta a punta (agregar y pagar) | Smoke |
| C04 | Cambiar la cantidad de un producto y ver el total actualizado | Sanity |
| C05 | Eliminar un producto del carrito y ver el total recalculado | Sanity |
| C06 | Aplicar un cupón del 10% sobre el total del carrito | Regresión selectiva |
| C07 | El resumen de pago muestra el mismo total que el carrito | Regresión selectiva |
| C08 | El carrito conserva productos y total al cerrar y abrir la app | Regresión selectiva |
| C09 | Cambiar la foto de perfil | No ejecutar |
| C10 | Recibir una notificación push de promoción | No ejecutar |
| C11 | Cambiar el idioma de la app | No ejecutar |

## Veredicto: NO-GO

La prueba sanity automatizada del fix pasó en el emulador Android 14: con 2 Audífonos BT el total del carrito da $59.98. Todavía no corrimos la regresión selectiva de cupones, resumen de pago y persistencia del carrito, que también llaman a recalcularTotal(), ni las otras 8 configuraciones de la matriz pairwise. Detenemos el build hasta completar esas pruebas, porque un error en el total afecta directamente lo que paga el cliente.
