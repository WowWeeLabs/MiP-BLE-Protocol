WowWee MiP Bluetooth Low Energy Protocol
===============

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
  - Send Data WRITE Characteristic: 0xFFE5
  
Using your Bluetooth Framework of choice you can choose to run a callback everytime you receive data using the Receive Data NOTIFY Characteristic.
  
**Controlling MiP**

All of the available control commands are located in [the command document](MiP-Protocol.md)

License
-----------------------------------------------

You are free to use this protocol document to release your own apps which can control MiP.
