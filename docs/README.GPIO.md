MPSSE GPIO
==========

Libmpsse supports toggling the FTDI chip's GPIO pins in SPI, I2C and GPIO modes.

This is done via the PinHigh and PinLow functions, which set the specified pin high or low respectively:

	gpio = MPSSE(GPIO)
	gpio.PinHigh(GPIOL0)
	gpio.PinLow(GPIOH1)
	gpio.Close()

The state of the first four GPIO pins (GPIOL0 - GPIOL3) can also be read using the ReadPins or PinState
functions. Note that unlike in BITBANG mode, you should specify the appropriate GPIOLx definition for the
GPIOL pin you wish to read, rather than the absolute pin number:

	gpio = MPSSE(GPIO)
	print "GPIOL0 State:", gpio.PinState(GPIOL0)
	gpio.Close()

The following GPIO pins are defined by libmpsse:

	GPIOL0
	GPIOL1
	GPIOL2
	GPIOL3

	GPIOH0
	GPIOH1
	GPIOH2
	GPIOH3
	GPIOH4
	GPIOH5
	GPIOH6
	GPIOH7

It should be noted that when in SPI or I2C modes, the GPIOL pins can only be set before a Start() or after
a Stop(); that is, they cannot be set in between calls to the Start() and Stop() functions. The GPIOH pins
can be set at any time.
