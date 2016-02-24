# spi-5wire
There are many 5 wire SPI variants in the wild. Most of them differ in a usage of 5. wire :)

## Variants of 5. wire usage
### Request only
Slave will signal Master that some data are present and should be read read out from slave.

### HW Flow control (Ready signal)
Slave will suggest SPI Master controller to start or pause transfer if slave internall buffer is note ready.
This is working only with kontrollers supporting it by HW or full SW (for example spi-gpio) implementation.

### SW Flow control + Request
Slave using same line to request transfer from Master. And ACK start and end of transfer.
This implementation was designed to work around low cost reqierements, limitiations of HW SPI controllers and SW latency.

## Patents
* CN102508812A https://www.google.de/patents/CN102508812A?cl=en&hl=de
* CN101552733B https://www.google.de/patents/CN101552733B?cl=en&hl=de&dq=spi_mrdy
