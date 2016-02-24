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

### SW Flow control + Request + (Ready signal)
Same as "SW Flow control + Request" and but can pause transfer. This implementation can be done only by HW controller.

## Patents
* CN102508812A https://www.google.de/patents/CN102508812A?cl=en&hl=de
* CN101552733B https://www.google.de/patents/CN101552733B?cl=en&hl=de&dq=spi_mrdy

## Common
At some point we can see that all this variants have common parts but different naming and combinations. Lets try to name it:
* Master Start Request - Master set CS_=0 and waiting for Slave DATA Start (if supported)
* Slave DATA Start - Slave (if CS_=0) set 5-wire_=0 to allow Master to start or resume data transfer
* Slave DATA Stop - Slave (if CS_=0) set 5-wire_=1,  to stop DATA transmission.
* Master end of transmission - Master set CS_=1 and waiting for "Slave end of transmission ACK" if supported.
* Slave end of transmission ACK - Slave (if CS_=1) set 5-wire_=1
* Slave Request - Slave (if CS_=1) set 5-wire_=0, *master should redirect request to spi_device driver*.
* Master Confirm request and start data transmission - if 5-wire_=0 set CS_=1 and transmit.
