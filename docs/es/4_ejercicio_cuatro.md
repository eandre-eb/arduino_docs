---
id: 4_ejercicio_cuatro
title: Ejercicio 4: "Conexión de un Servo motor"
---

## Ejercicio 4: "Conexión de un Servo motor"

### Objetivo General

Conectar un servo motor en Arduino.

### Materiales

- Placa Arduino Uno-R3
- Un cable USB tipo A/B de impresora
- Una computadora
- Servo SG90
- Breadboard/Protoboard
- Jumper Wires

### Código


```
#include <Servo.h>

Servo servo;

int initial = 0;

void setup() {
  servo.attach(8);
  servo.write(initial);
}

void loop() {
  // scan from 0 to 180 degrees
  for(int angle = 10; angle < 180; angle++) {
      servo.write(angle);
      delay(15);
  }
  // now scan back from 180 to 0 degrees
  for(int angle = 180; angle > 10; angle--) {
      servo.write(angle);
      delay(15);
  }
}
```

### Esquema de Montaje

<img src="https://educ8s.tv/wp-content/uploads/2016/01/servo_bb.png" alt="">

- Marrón = GND / Negativo
- Rojo = Positivo
- Amarillo = Señal principal

## Fuente:

* http://educ8s.tv/arduino-servo-tutorial/