nvm.toml
============

[![Discord](https://img.shields.io/discord/327254708534116352.svg)](https://adafru.it/discord)
[![Build Status](https://github.com/adafruit/cascadetoml/workflows/Build%20CI/badge.svg)](https://github.com/adafruit/nvm.toml/actions)

This is a human and machine readable "database" of config for non-volatile memory chips. It uses [`cascadetoml`](https://github.com/adafruit/cascadetoml) to allow common technology and manufacturer settings to be shared amongst all SKUs.

Shared data goes in a toml file with a name that matches the folder name.

The [template](nvm.template.toml) documents all of the possible fields.

Example
==========

Single SKU
-----------

To get the TOML for a specific SKU do:

```shell
cascadetoml cascade filter sku=\"GD25Q64C\"
```

Here is example TOML output:

```toml
[[nvm]]
# Data for path: flash/gigadevice/GD25Q64C.toml

# Data inferred from the path: {technology}/{manufacturer}/{sku}.toml
technology = "flash"
manufacturer = "gigadevice"
sku = "GD25Q64C"

# Data from flash/flash.toml
supports_fast_read = true

# Data from flash/gigadevice/GD25Q64C.toml
# Settings for the Gigadevice GD25Q64C 8MiB SPI flash.
# Datasheet: http://www.elm-tech.com/en/products/spi-flash-memory/gd25q64/gd25q64.pdf
total_size = 0x800000 # 8 MiB
capacity = 0x17
write_status_register_split = true
```

All from one Manufacturer
--------------------------

The filters are actually TOML themselves. They match any entry that include the given keys with any of the given values.

To get all `gigadevice` flashes you'd run:

```shell
cascadetoml cascade filter manufacturer=\"gigadevice\"
```

Cascade walk-through
=====================

The paths all match `{technology}/{manufacturer}/{sku}.toml`. A file such as `flash/gigadevice/GD1.toml` will have the implicit values:

```toml
technology = "flash"
manufacturer = "gigadevice"
sku = "GD25Q64C"
```

All of the other values come from these files in order:

* `flash/flash.toml`
* `flash/gigadevice/gigadevice.toml`
* `flash/gigadevice/GD25Q64C.toml`

Contributing
============

Contributions are welcome! Please read our [Code of Conduct](https://github.com/adafruit/Adafruit_CircuitPython_cascadetoml/blob/main/CODE_OF_CONDUCT.md)
before contributing to help this project stay welcoming.

Documentation
=============

For information on building library documentation, please check out
[this guide](https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1).
