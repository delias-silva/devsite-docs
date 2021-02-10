---
sites_supported:
  - mla
  - mlm
  - mlb
---

# Lógica de reintentos de cobro

Al automatizar la recurrencia de tus cobros, se crean pagos autorizados que tendrán una fecha de débito configurada en base a la periodicidad que se definió en la suscripción. 

## Estados de pago

----[mla]----
En el momento en que se cobre la cuota pueden surgir tres alternativas en base al resultado de su pago:
------------

----[mlb, mlm]----
En el momento en que se cobre la cuota pueden surgir dos alternativas en base al resultado de su pago:
------------

* __El pago es realizado exitosamente__ por lo que la cuota quedará `processed` y ya no se reintentará cobrarla. 
----[mla]----
* __El pago se está procesando__ por lo que la cuota quedará en `waiting for gateway` hasta que se resuelva el pago.
------------
* __El pago es rechazado__ por lo que la cuota quedará en `recycling` siempre y cuando la cuota no esté expirada o no haya alcanzado el máximo de reintentos. Caso contrario, quedará en `processed`.


## Pagos rechazados

Cuando una cuota queda en el estado `recycling` entra en un esquema de reintentos con un máximo de 4 posibilidades, en los que se vuelve a realizar el cobro de la cuota. El resultado puede ser cualquiera de los tres puntos mencionados arriba. 

Si el pago resulta rechazado, se actualiza a una nueva fecha de cobro sumando 1 de las 4 posibilidades dentro de los diez días como ventana de tiempo de reintento a la última fecha de disponible.

Por defecto se reintenta dentro de una ventana de 10 días. En caso de que la cuota tenga fecha de expiración, la ventana de tiempo se ajusta a esa fecha y mantiene la lógica de 4 reintentos.

----[mla]----

## Pagos en proceso

Si una cuota se encuentra en el estado `waiting for gateway` y cuando se resuelve el pago resulta rechazada y se cumplió la fecha de expiración, la cuota automáticamente pasará a procesada con el estado `processed`. Caso contrario, entrará al esquema de reintento.

------------

En el caso de que no se pueda cobrar la cuota en el cuarto reintento, la cuota automáticamente quedará en el estado `processed` asociada a un pago rechazado.

> NOTE
> 
> Nota
> 
> El resultado de una cuota no afecta la generación y procesamiento del resto de las cuotas para la misma suscripción.

------------
### Próximos pasos

> LEFT_BUTTON
>
> Integración avanzada
>
> Actualiza, modifica o cancela tus suscripciones.
>
> [Integración avanzada](https://www.mercadopago[FAKER][URL][DOMAIN]/developers/es/guides/online-payments/subscriptions/advanced-integration)

> RIGHT_BUTTON
>
> Pruebas
>
> Revisa que tus suscripciones creadas estén bien configuradas con los usuarios de prueba. 
>
> [Pruebas](https://www.mercadopago[FAKER][URL][DOMAIN]/developers/es/guides/online-payments/subscriptions/testing)
