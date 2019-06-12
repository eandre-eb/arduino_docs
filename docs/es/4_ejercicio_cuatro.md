---
id: 4_ejercicio_cuatro
title: Ejercicio 4: "Conexión de un Servomotor"
---

## Ejercicio 4: "Conexión de un Servomotor"

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

## Anexos

### ¿Qué es un Servomotor?

<img src="https://i.ytimg.com/vi/LXURLvga8bQ/maxresdefault.jpg" alt="">

Un servomotor (también llamado servo) es un dispositivo similar a un motor de corriente continua que tiene la capacidad de ubicarse en cualquier posición dentro de su rango de operación, y mantenerse estable en dicha posición.1​

El servomotor es un motor eléctrico lleva incorporado un sistema de regulación que puede ser controlado tanto en velocidad como en posición.

Es posible modificar un servomotor para obtener un motor de corriente continua que, si bien ya no tiene la capacidad de control del servo, conserva la fuerza, velocidad y baja inercia que caracteriza a estos dispositivos.

Está conformado por un motor y un circuito de control. También potencia proporcional para cargas mecánicas. Un servo, por consiguiente, tiene un consumo de energía reducido.

La corriente que requiere depende del tamaño del servo. Normalmente el fabricante indica cuál es la corriente que consume. La corriente depende principalmente del par, y puede exceder un amperio si el servo está enclavado.

En otras palabras, un servomotor es un motor especial al que se ha añadido un sistema de control (tarjeta electrónica), un potenciómetro y un conjunto de engranajes. Con anterioridad los servomotores no permitían que el motor girara 360 grados, solo aproximadamente 180; sin embargo, hoy en día existen servomotores en los que puede ser controlada su posición y velocidad en los 360 grados. Los servomotores son comúnmente usados en modelismo como aviones, barcos, helicópteros y trenes para controlar de manera eficaz los sistemas motores y los de dirección.


**Pros y contras de DC, servo y motor paso a paso**

Las ventajas y desventajas del motor de corriente continua, el servomotor y el motor paso a paso incluyen lo siguiente.

- Los motores de CC son rápidos y los motores de rotación continua se utilizan principalmente para cualquier cosa que necesite girar a una alta rotación por minuto (RPM). Por ejemplo; ruedas de coche, ventiladores etc.

- Los servomotores son de alto par, rotación rápida y precisa en un ángulo limitado. En general, una alternativa de alto rendimiento a los motores paso a paso, pero una configuración más complicada con el ajuste de PWM. Adecuado para brazos / piernas robóticos o control del timón, etc.

- Los motores paso a paso son lentos, de fácil configuración, rotación precisa y control: ventaja sobre otros motores como los servomotores para controlar una posición. Donde estos motores requieren un mecanismo de retroalimentación y un circuito de respaldo para conducir la ubicación, este motor tiene control posicional a través de su naturaleza de rotación por adiciones fraccionarias. Adecuado para impresoras 3D y dispositivos relacionados donde la posición es esencial.

## Fuente:

* http://educ8s.tv/arduino-servo-tutorial/
* https://www.elprocus.com/difference-dc-motor-servo-motor-stepper-motor/