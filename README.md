libmpsse
========

Open source library for SPI/I2C control via FTDI chips. Supports
FTDI chips that contain an MPSSE engine, such as the FT-2232H and the FT-232H.


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

