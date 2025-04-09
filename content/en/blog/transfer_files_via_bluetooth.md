+++
title = "Transfer files via Bluetooth in the terminal"
description = "Transfer files via Bluetooth in the terminal"
date = 2025-04-09
tags = [
    "tech",
    "guide",
	"bluetooth"
]
+++

1. Install dependencies: `pacman -S bluez-utils bluez-tools bluez-obex`

2. Pairing devices:

```sh
bluetoothctl scan on
bluetoothctl pair <MAC>
```

3. Receiving files: `bt-obex -s ~/Downloads`

4. Sending files: `bt-obex -p <MAC> filename.txt`
