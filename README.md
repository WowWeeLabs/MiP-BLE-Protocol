WowWee MiP Bluetooth Low Energy Protocol
===============
[![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/WowWeeLabs/MiP-BLE-Protocol?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

![](Images/MiP.png)

The free MiP BLE protocol lets you send and receive commands to and from your [MiP robot](http://www.meetmip.com). You will need to write your own control code in the language of your choice using an appropriate Bluetooth Low Energy library.

Pre-built SDKs are available for iOS: https://github.com/WowWeeLabs/MiP-iOS-SDK

For information on WowWee products visit: http://www.wowwee.com/.

How to use it
-----------------------------------------------

**Finding a MiP before Connecting**

To know the difference between MiP and other BLE based products you can check the *Manufactorer Specific Data* which is sent as part of the advertising Packet. Check with your BLE framework on how to get this.

Each WowWee BLE product assigns a special 16bit ID in the first two bytes of the Manufactorer specific data. If you are using one of our prebuilt SDKs this is handled automatically for you.

**Connecing to a MiP**

Bluetooth Low Energy is made up of a series of Services & Characteristics. In the case of MiP these are proprietary which means you need to find them by UUID. The following important services are available:

- Receive Data Service: 0xFFE0
  - Receive Data NOTIFY Characteristic: 0xFFE4
- Send Data Service: 0xFFE5
  - Send Data WRITE Characteristic: 0xFFE9
  
Using your Bluetooth Framework of choice you can choose to run a callback everytime you receive data using the Receive Data NOTIFY Characteristic.

_**IMPORTANT**_

Sending command bytes is very easy, just send a raw byte according to the value in the table.

Receiving commands on the other hand need some special treatment before they can be processed as raw command bytes. All commands come in an ASCII encoded string. For example, in Objective-C you might do the following:

```objective-c
// Get ASCII command value from incoming data
NSString *ascii = [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];

// Here we simply split the string array for every 2 characters
NSMutableArray *theDataArray = [NSMutableArray array];
for (int i = 0; i < [asciiHex length]; i=i+2) {
  NSString *cmd = [asciiHex substringWithRange:NSMakeRange(i, 2)];
  [theDataArray addObject:@([cmd hexFromString])];
}

NSUInteger cmdByte = [theDataArray[0] unsignedIntegerValue];
[theDataArray removeObjectAtIndex:0];
NSUInteger length = [theDataArray count];

// Using the above code we can get the command
NSLog(@"The command is: %lu", cmdByte);
NSLog(@"Contains %lu extra data bytes: %@", length, theDataArray);
```

Note that this is just an example, you can use any language to processes commands if you follow these steps:

1. Convert the incoming string to ASCII
2. Process the ASCII string and split it off every 2 characters, every two characters is a single incoming hex byte
3. Convert each string set of hex characters into a integer value

Process incoming integer values as you would normally based on the command protocol document.

**Controlling MiP**

All of the available control commands are located in [the command document](MiP-Protocol.md)

**Exciting Projects**

We always love to share great projects that are built off of our libraries, so far here are the ones we know about:

* [Cyon-MiP](https://github.com/hybridgroup/cylon-mip) - A NodeJS library for controlling MiP

If you've developed your own library or project please send us a pull request!
