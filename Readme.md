#PRÁCTICA 3B: Comunicación bluetooth con el movil

##Apartado 1

###Codigo

```
#include "BluetoothSerial.h"

#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif

BluetoothSerial SerialBT;

void setup() {
  Serial.begin(115200);
  SerialBT.begin("ESP32test"); //Bluetooth device name
  Serial.println("The device started, now you can pair it with bluetooth!");
}

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

#Funcionamiento

Primero de todo cargamos la libreria BluetoothSerial :

`#include "BluetoothSerial.h"`

Una vez cargada la libreria, se comprueba si el Bluetooth esta habilitado:

```
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
```
Creamos una instancia de `BluetoothSerial` con el nombre de `SerialBT` :

`BluetoothSerial SerialBT;`

En la primera linea del void setup inicializamos una comunicación serie con una velocidad de 115200 bauds `Serial.begin(115200);`.

Seguidamente se inicializa el dispositivo serie Bluetooth y pasamos el nombre del dispositivo:

`SerialBT.begin("ESP32test");`

y en la ultima linea en el setup() escribes que ya has inicializado el dispositivo:

`
Serial.println("The device started, now you can pair it with bluetooth!");
}
`

Por ultimo, creamos el void loop donde crearemos un if para verificar si se estan recibiendo bytes en el puerto serie:

```
if (Serial.available()) {
SerialBT.write(Serial.read());
}
```

En el segundo if se comprueba si hay bytes disponibles para leer en el puerto serie Bluetooth:

```
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
```

Para finalizar el loop, se crea una delay:

`delay(20);`

#Salida por el terminal


![4](https://i.ibb.co/8br1mLd/Salida.jpg)



