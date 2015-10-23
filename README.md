libmpsse
========

Libmpsse is a library for interfacing with SPI/I2C devices via FTDI's FT-2232
family of USB to serial chips. Additionally, it provides control over the
GPIO pins on the FTDI chips and supports a raw bitbang mode as well. Based
around the libftdi library, it is written in C and includes a Python wrapper
courtesy of swig.

Install
-------

This library installs like a traditional package:

    cd src
    ./configure
    make
    sudo make install

By default, it will install for the version of Python that your `python`
executable points to. To specify the version, run configure with some
environment variables set:

    PYDEV=/usr/include/python3.4 PYLIB=/usr/local/lib/python3.4/dist-packages ./configure
    make
    sudo make install



Usage
-----

The following Python code demonstrates using libmpsse to read 256 bytes
from a standard SPI flash chip:

```python
from mpsse import *

flash = MPSSE(SPI0, TEN_MHZ, MSB)
flash.Start()
flash.Write("\x03\x00\x00\x00")
data = flash.Read(256)
flash.Stop()
flash.Close()
```


To toggle a GPIO pin:

```python
import mpsse
from time import sleep

# Open mpsse in GPIO mode
io = mpsse.MPSSE(mpsse.GPIO)

print('got device')

# Toggle the first GPIO pin on/off 10 times
while True:
	io.PinHigh(mpsse.GPIOL0)
	print('GPIOL0 State: {}'.format(io.PinState(mpsse.GPIOL0)))
	sleep(1)

	io.PinLow(mpsse.GPIOL0)
	print('GPIOL0 State: {}'.format(io.PinState(mpsse.GPIOL0)))
	sleep(1)

io.Close()
```

