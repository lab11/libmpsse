MPSSE Bitbang
=============

Libmpsse supports a raw bitbang mode that provides full control over the eight DBUS pins of each interface
on the FTDI chip. The DBUS pins are the first eight pins on each FTDI interface.

Pins can be set high or low using the PinHigh and PinLow functions respectively:

	bitbang = MPSSE(BITBANG)
	bitbang.PinHigh(0)
	bitbang.PinLow(7)
	bitbang.Close()

Pin values can be read using the ReadPins and PinState functions. ReadPins returns an integer with the bits
respective to each pin set to a 1 if the pin is high or a 0 if the pin is low:

	pins = bitbang.ReadPins()

	if (pins & (1 << 0)):
		print "Pin 0 is high!"
	else:
		print "Pin 0 is low!"

Alternatively, the PinState function can be used to check the state of a given pin:

	pins = bitbang.ReadPins()

	if bitbang.PinState(0, pins) == 1:
		print "Pin 0 is high!"
	else:
		print "Pin 0 is low!"

If the 'pins' value is set to -1 when calling PinState, then PinState will call ReadPins automatically:

	if bitbang.PinState(0, -1) == 1:
		print "Pin 0 is high!"
	else:
		print "Pin 0 is low!"

Valid pin numbers for all of the above functions when in BITBANG mode are 0 through 7.
