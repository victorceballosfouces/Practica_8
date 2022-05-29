# Practica_8
Para la práctica hemos tenido que desarrollar un código sencillo con el cual poder enviar datos por el bus UART0 que hay en el esp32 y recibirlos por el UART2 conectado a las salidas GPIO. Una vez recibidos, enviarlos otra vez al UART0.
## Codigo
```cpp
#include <Arduino.h>
 
 
void setup() {
 Serial.begin(115200);
  Serial2.begin(115200);
}
 
void loop() { //Choose Serial1 or Serial2 as required
 while (Serial.available()) {
   Serial2.print(char(Serial.read()));
 }
 while (Serial2.available()) {
   Serial.print(char(Serial2.read()));
 }
}
```
## Funcionamiento
Primero creamos dos objetos serial 1 y 2, configurandolos con el mismo baud rate para conseguir cortocircuitarlos. Ya en el loop(), que es donde se desarrollara la función principal de este programa, miramos si tenemos algo disponible para leer en el primer serial. Eso que se encuentra en el 1 será escrito por pantalla por el 2, y debido a que los puertos de los dos estan conectados tanto para transmitir como recibir datos  también se recibirá en el mismo serial 2 cuando hagamos su avaliable().

Para finalizar realizamos el mismo proceso al revés pero con el mismo resultado, leyendo con la función read lo que hay en el buffer del UART2 (serial 2) y escribiendolo por el puerto UART0 (serial 1).
