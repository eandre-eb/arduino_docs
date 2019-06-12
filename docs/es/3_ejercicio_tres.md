---
id: 3_ejercicio_tres
title: Ejercicio 3: "Velocidad y Dirección de un Motor CC"
---

## Ejercicio 3: "Velocidad y Dirección de un Motor CC"

### Objetivo General

Controlar la velocidad y dirección de giro de un motor de corriente contínua con el driver L293D.

### Materiales

- Placa Arduino Uno-R3
- Un cable USB tipo A/B de impresora
- Una computadora
- Motor de corriente contínua (CC)
- [L293D Driver](http://pdf1.alldatasheet.com/datasheet-pdf/view/22432/STMICROELECTRONICS/L293D.html)
- Breadboard/Protoboard
- Jumper Wires
- Batería 9v

### Parte 1: Dirección

**Código**

```
int dir1 = 8;
int dir2 = 9;

void setup() {
  pinMode(dir1,   OUTPUT);
  pinMode(dir2,   OUTPUT);
}

void loop() {
  digitalWrite(dir1, HIGH);
  delay(3000);
  digitalWrite(dir1, LOW);
  delay(3000);
  digitalWrite(dir2, HIGH);
  delay(3000);
  digitalWrite(dir2, LOW);
  delay(3000);
}
```

### Esquema de Montaje

**1 Motor**
<img src="https://lh3.google.com/u/0/d/1oDrwRwdWpnj-36RiSDgZYwBbP7odgpBy=w2880-h1578-iv2" alt="">

**2 Motores**
<img src="https://lh3.google.com/u/0/d/1tiCooirbYLpjnbVBPKs071bjgH_VUSp3=w1710-h1578-iv2" alt="">



### Parte 2: Velocidad

**Código**

```
int m1 = 8;
int pot = A0;
int speed;

void setup(){
  Serial.begin(9600);
  pinMode(m1, OUTPUT);
  pinMode(pot, INPUT);
}

void loop(){
  speed = (analogRead(pot)/4);
  Serial.print("speed: \n ");
  Serial.print(speed);

  analogWrite(m1, speed);

}
```
### Esquema de Montaje

<img src="https://lh3.google.com/u/0/d/19JO2C6iI8J1UvHg5NFagifuBuR3ut2Gp=w2880-h1578-iv2" alt="">


## Fuente:

* http://ohhmyproject.blogspot.com/2015/09/tutorial-l293d-motor-driver-with-arduino.html