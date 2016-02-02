WowWee MiP Linux GATT Explanation
===============
This is a work in progress.  At the moment all it does is explain how to use linux
command line tools to connect to your WowWee MiP and send it basic commands.

**Install Dependencies (Ubuntu)**


How to use it
-----------------------------------------------
**Finding a MiP before Connecting**

```
$sudo hcitool lescan
[sudo] password for gherlein:
LE Scan ...
55:52:21:D9:16:36 (unknown)
55:52:21:D9:16:36 (unknown)
1C:05:FE:F5:B2:A3 (unknown)
1C:05:FE:F5:B2:A3 Mip-14915
```

**Connecting to a MiP**

First, make it easy to use the MiP Bluetooth address in commands:

```
$BTADDR=1C:05:FE:F5:B2:A3
```

Note that 0xFFE9 is the characteristic for the Send Data Service (see
https://github.com/WowWeeLabs/MiP-BLE-Protocol/blob/master/MiP-Protocol.md).
We'll look for the handle for that service.

```
$sudo gatttool -b $BTADDR --characteristics | grep ffe9
handle = 0x001a, char properties = 0x0c, char value handle = 0x001b, uuid = 0000ffe9-0000-1000-8000-00805f9b34fb
```
we need the "handle = 0x001b" data for the next step.

**Controlling MiP**

We'll reference the commands from here:  https://github.com/WowWeeLabs/MiP-BLE-Protocol/blob/master/MiP-Protocol.md

```
$ sudo gatttool -b $BTADDR -I
[   ][1C:05:FE:F5:B2:A3][LE]> connect
[CON][1C:05:FE:F5:B2:A3][LE]> char-write-cmd 0x001b 7000FF010000
```

The first line connects to the MiP.  You should see the chest LED turn green.
The next line sends a command to the handle we identified in the last step. The
hex series of 7000FF010000 is command 70 (Distance Drive).  The next series of bytes
are forward (00) for max distance (FF) with a clockwise turn (01) of no degrees (0000).

You can experiment with other commands.



