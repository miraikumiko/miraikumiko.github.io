+++
title = "Your own Monero payment gateway"
description = "Creating your own anonymous payment gateway"
date = 2025-03-19
tags = [
    "tech",
    "guide",
    "monero"
]
+++

Creating your own Monero payment gateway is very easy, here are the main steps:

1. Run `monero-wallet-rpc --tx-notify "script.sh %s"`, where **%s** is **txid**, which will be automatically passed to your script as the first argument. Your script will be executed with each received transaction.

2. When a buyer, for example in your online store, wants to pay for a product, the site should give him an address to which the money will be transferred. To do this, your web application must perform an RPC request [make_integrated_address](https://docs.getmonero.org/rpc-library/wallet-rpc/#make_integrated_address) to the daemon you launched to receive such an address **integrated_address** and **payment_id**. The address is given to the buyer, and the payment identifier is saved for future verification.

3. After the money is transferred, your script from the first point will receive **txid** which must be passed to your web application. It will receive **payment_id** and **amount** using the RPC method [get_transfer_by_txid](https://docs.getmonero.org/rpc-library/wallet-rpc/#get_transfer_by_txid) — the identifier and amount of the payment.

4. The application checks the payment ID and the received amount, which is measured in atomic units 1 XMR = 1e12 (atomic-units). Keep this in mind when comparing the amount, it is written at the beginning of the [documentation](https://docs.getmonero.org/rpc-library/wallet-rpc).

Making one-time payments without an internal balance is very inconvenient, so it is best to create a user balance in the database on the site, which can be replenished at any time.
