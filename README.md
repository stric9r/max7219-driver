# max7219-driver
Serially interfaced 8 digit LED display driver

The implementation of this is with GPIO only, bit banging the chip instead of relying on a serial interface.
There is a branch open now that has the ability to use SPI, but it is untested.  

## General
This driver is for the max7219 serial display driver.  See datasheet in this repository for more details of how the chip functions.
See this repository for an example of how this is used: https://github.com/stric9r/Line6-FBV3-Clone


