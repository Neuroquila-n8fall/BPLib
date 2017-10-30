BPLib - Bluetooth SPP/HID Library
=====

This library simplifies using the RN-42 Bluetooth Module ([or the $3 HC-05/6 flashed with RN-42 firmware](https://youtu.be/y8PcNbAA6AQ)).

The main advantage of the RN-42 module is it allows you to emulate HID devices, which allows your Arduino project to connect to your devices as a Bluetooth keyboard, mouse or gamepad.

This library is forked from this one [here](https://github.com/baselsw/BPLib), the main differences between this one and the original is that hardcoded references to a serial interface have been removed so it can be used with basically any Arduino device.

## Usage

Basic usage of the library is as shown, this sketch when connected to your device will send the key commands "H" and "i" every 5 seconds.

```
#include <BPLib.h>
BPLib *BPMod;

void setup(){
  Serial.begin(115200); // 115200 is the default baud of the RN-42
  BPMod = new BPLib(Serial);
  BPMod->begin(BP_MODE_HID,BP_HID_KEYBOARD);   //Begin HID Mode with HID KEYBOARD AS TYPE

}

void loop(){
  delay(5000);
  BPMod->sendString("Hi");
}
```

The library also supports connecting using software serial interfaces.

```
#include <SoftwareSerial.h>
SoftwareSerial swSer(1, 2, false, 128);

....

void setup(){
  swSer.begin(115200);
  BPMod = new BPLib(swSer);
  BPMod->begin(BP_MODE_HID,BP_HID_KEYBOARD);
}

...
```

It is also worth noting that the **BPMod->begin** method is a once off configuration, if you do it for your module once it does not need to be run again, even after reboots, so it does not need to be part of your final sketch.

## Examples

- [Keyboard - Using software serial](https://github.com/witnessmenow/BPLib/blob/master/examples/HID_KEYBOARD/HID_KEYBOARD.ino)
- [Mouse](https://github.com/witnessmenow/BPLib/blob/master/examples/HID_MOUSE/HID_MOUSE.ino)
- [Mouse Wheel](https://github.com/witnessmenow/BPLib/blob/master/examples/HID_MOUSE_WHEEL/HID_MOUSE_WHEEL.ino)
- [Basic serial connection](https://github.com/witnessmenow/BPLib/blob/master/examples/SPP_SEND_REC_MSG/SPP_SEND_REC_MSG.ino)


## Details

Check out the [header file of the library](https://github.com/witnessmenow/BPLib/blob/master/src/BPLib.h) for a full list of functions and parameters available. If you have suggests on how to present this better please feel free to submit a PR!
