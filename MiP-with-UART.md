Using MiP from UART
===============

MiP contains a UART serial port which can receive the same commands as the Bluetooth Low Energy receiver. After you connect to the TX & RX pins on the PCB you need to send the byte 0xFF, once this is sent you can send the commands as per the BLE documentation.

To connect to MiP you need to use these settings:

* Baud Rate: 115200
* Flow Control: Off
* Data Bits: 8
* Parity Bit: None
* Stop Bit: 1

**Python Example**

Thanks to [rjelbert](https://github.com/rjelbert) for the sample code.

```python

import serial
import time
ser = serial.Serial('/dev/ttyAMA0', 115200)
time.sleep(0.1)

init MIP in serial mode

ser.write(b'\xFF')

```

set front LED to flashing GREEN

```python

time.sleep(0.1)
ser.write(b'\x89')
ser.write(b'\x00')
ser.write(b'\xFF')
ser.write(b'\x00')
ser.write(b'\x01')
ser.write(b'\x10')
time.sleep(10)

```

now send MIP to sleep

```python

ser.write(b'\xFA')
ser.flush()

```

**Arduino Example**

Thanks to [timab25](https://github.com/timab25) here is some sample code for Arduino Mega that uses Serial1 to init, make chest blink green, then sleep.

*Note:* The delay after sending the init is needed.

```arduino

//Setup Serial1 for correct baud rate

Serial1.begin(115200);

//Send init command
Serial1.write(0xFF);
delay(30); // delay in between reads for stability

//Send command to blink chest green
Serial1.write(0x89);
Serial1.write(0x00);
Serial1.write(0xFF);
Serial1.write(0x00);
Serial1.write(0x01);
Serial1.write(0x10);
delay(30000);

//Send command to sleep
Serial1.write(0xFA);

```
