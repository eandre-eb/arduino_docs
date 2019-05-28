---
id: 2_ejercicio_dos
title: Ejercicio 2: "Ultrasonic Distance Sensor"
---

## Ejercicio 2: "Ultrasonic Distance Sensor" - Sensor ultrasónico de distancia

### Objetivo General

- En éste ejercicio vamos a aprender a utilzar el sensor ultrasónico HC-SR04 y como usarlo con un Buzzer y un LED.

### Materiales

- Placa Arduino Uno-R3
- Un cable USB tipo A/B de impresora
- Una computadora
- Sensor ultrasónico HC-SR04
- Breadboard/Protoboard
- Jumper Wires
- Buzzer
- LED
- Resistencia de 220 Ohm

### Código

```
// defines pins numbers
const int trigPin = 9;
const int echoPin = 10;
const int buzzer = 11;
const int ledPin = 13;

// defines variables
long duration;
int distance;
int safetyDistance;


void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(buzzer, OUTPUT);
pinMode(ledPin, OUTPUT);
Serial.begin(9600); // Starts the serial communication
}


void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance <= 5){
  digitalWrite(buzzer, HIGH);
  digitalWrite(ledPin, HIGH);
}
else{
  digitalWrite(buzzer, LOW);
  digitalWrite(ledPin, LOW);
}

// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
}
```

Para probar este código, conecta tu arduino, asegúrate de que el puerto esté correctamente configurado, verifica el código (compila) y luego cárgalo. Verás como el LED integrado a la arduino comienza a parpadear cada un segundo.


Conexiones:

El módulo ultrasónico HC-SR04 tiene 4 pins, Ground, VCC, Trig and Echo. El pint Ground y VCC necesitan ser conectados al pin de Ground y de 5 volts de la placa Arduino respectivamente y los pins trig y echo a cualquier pin Digital I/O de la placa Arduino.

* Sensor HC-SR04 conectarlo a la Breadboard
* Pin VCC del sensor conectarlo al pin +5V del Arduino
* Pin GND del sensor conectarlo al pin GND del Arduino
* Pin Trig del sensor conectarlo al pin Digital I/O #9 del Arduino
* Pin Echo del sensor conectarlo al pin Digital I/O #10 del Arduino

**Buzzer y LED**
* Conectar el Buzzer a la Breadboard
* La pata larga (+) del Buzzer long leg  conectarla al pin Digital I/O #11 del Arduino
* La pata corta (-) del Buzzer conectarla al pin GND del Arduino
* Conectar el LED a la Breadboard
* Conectar la Resistencia a la pata larga (+) del LED
* Conectar la otra pata de la resistencia (de la pata larga del LED) al pin Digital #13 del Arduino
* A la pata corta (-) del LED conectarla al pin GND del Arduino

Esquemático:

<img src="https://lh3.google.com/u/0/d/1WklsRgIqXQrclYSXZOLPwCSz_VxoqboX=w1710-h1546-iv1" width="700">

