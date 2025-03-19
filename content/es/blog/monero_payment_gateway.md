+++
title = "Propio sistema de pago Monero"
description = "Crea tu propio sistema de pago anónimo"
date = 2025-03-19
tags = [
    "tech",
    "guide",
    "monero"
]
+++

Crear tu propio sistema de pago Monero es muy fácil, aquí tienes los pasos básicos:

1. Ejecute `monero-wallet-rpc --tx-notify "script.sh %s"`, donde **%s** es el **txid** que se pasará automáticamente a su script como primer argumento. Su script se ejecutará con cada transacción recibida.

2. Cuando un comprador, por ejemplo en tu tienda online, quiere pagar un producto, el sitio debe darle la dirección a la que se transferirá el dinero. Para hacer esto, su aplicación web debe realizar una solicitud RPC [make_integrated_address](https://docs.getmonero.org/rpc-library/wallet-rpc/#make_integrated_address) al demonio que está ejecutando para obtener la **integrated_address** y la dirección **payment_id**. La dirección se proporciona al comprador y el ID de pago se almacena para verificación futura.

3. Después de transferir el dinero, su secuencia de comandos desde el primer punto recibirá **txid** que deberá pasar a su aplicación web. Usando el método RPC [get_transfer_by_txid](https://docs.getmonero.org/rpc-library/wallet-rpc/#get_transfer_by_txid) recibirá **payment_id** y **amount** — el identificador y el monto del pago.

4. La aplicación verifica el ID de pago y el monto recibido, que se mide en unidades atómicas 1 XMR = 1e12 (unidades atómicas). Tenga esto en cuenta al comparar la cantidad, esto está escrito al comienzo de la [documentación](https://docs.getmonero.org/rpc-library/wallet-rpc).

Realizar pagos únicos sin un saldo interno es muy inconveniente, por lo que es mejor crear un saldo de usuario en la base de datos del sitio, que se puede reponer en cualquier momento.
