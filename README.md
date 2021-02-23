Particle ST7789 example
===

### screen
MakerFocus TFT LCD Screen Display 1.3inch TFT LCD Module, 240240 IPS 65K Full Color 3.3V with SPI Interface ST7789 IC Driver

https://www.amazon.com/gp/product/B07P9X3L7M

- 240x240
- No chip select
- 3.3v

### board
Particle 3rd gen

### pins
|screen|particle|
|:----:|:------:|
|SDA | MO|
|SCL | SCK|
|RES | D6|
|DC  | D5|
|VCC | 3.3|
|GND | GND|

### driver
- [Adafruit ST7789 library](https://www.arduino.cc/reference/en/libraries/adafruit-st7735-and-st7789-library/)
- [Adafruit GFX v1.10.3](https://github.com/adafruit/Adafruit-GFX-Library)
- with Conan https://github.com/hicktech/conan-AdafruitGFX

### conan
`PLATFORM=xenon VERSION_STRING=1.4.2 conan install . -if cmake-build-debug -s compiler.version=5.3 -s os=Particle -s os.board=xenon -s arch=nRF52840 -s compiler.libcxx=libstdc++11`

### build
```
arm-none-eabi-size --format=berkeley src.elf
   text	   data	    bss	    dec	    hex	filename
  26888	    108	   1188	  28184	   6e18	src.elf
```

### flash
`./cmake-build-debug/flash src usb`

### notes
The product page [says to modify `Adafruit_SPITFT.cpp`](doc/img.png) but this is likely referenced from an older version of the library.

It can be set with the init call, see `setup()` in the call to `tft.init`

`tft.init(240, 240, SPI_MODE3);`

The product page also says connect to 5v but it appears to run fine from 3.3v.
