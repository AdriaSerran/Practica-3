# Practica-3 WIFI Y BLUETOOTH

En aquesta part de la pràctica farem servir una aplicació pel mòbil, amb aquesta escriurem des de l'ordinador i ens sortirà al xat que tindrem al mòbil i viceversa.

# Material
- ESP32
- Mòbil

# Funcionament

Farem els includes i iniciarem el BluetoothSerial com a SerialBT.

```c++
#include <Arduino.h>
//This example code is in the Public Domain (or CC0 licensed, at your option.)
//By Evandro Copercini - 2018
//
//This example creates a bridge between Serial and Classical Bluetooth (SPP)
//and also demonstrate that SerialBT have the same functionalities of a normal Serial
#include "BluetoothSerial.h"
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
BluetoothSerial SerialBT;
```

Seguidament entrarem al setup on com sempre inicialitzarem el port sèrie i emparellarem el nostre mòbil amb l'ESP32.

```c++
void setup() {
Serial.begin(115200);
SerialBT.begin("ESP32test"); //Bluetooth device name
Serial.println("The device started, now you can pair it with bluetooth!");
}
```

Per últim, dins del loop el que farà és llegir el que s'està teclejant des de l'ordinador i ho enviarà cap al xat on es podrà veure des del mòbil.

```c++
void loop() {
if (Serial.available()) {
SerialBT.write(Serial.read());
}
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
delay(20);
}
```



https://user-images.githubusercontent.com/101885469/171615354-72283c9a-5ec5-41b8-82e4-0e097e1d22c2.mp4

