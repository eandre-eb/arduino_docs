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

### Intro

**Leyendo un potenciómetro (entrada analógica)**

Un potenciómetro es simplemente una resistencia variable, que  podemos leer desde Arduino como un valor analógico. En este ejemplo, ese valor controla la velocidad a la que parpadea un LED.

Conectamos tres cables a la placa Arduino. El primero va a tierra desde uno de los pines externos del potenciómetro. El segundo va de 5 voltios al otro pin externo del potenciómetro. El tercero va desde la entrada analógica 2 hasta el pin central del potenciómetro.

Al girar el eje del potenciómetro, cambiamos la cantidad de resistencia a cada lado del limpiador que está conectado al pin central del potenciómetro. Esto cambia la "cercanía" relativa de ese pin a 5 voltios y tierra, lo que nos da una entrada analógica diferente. Cuando el eje se gira completamente en una dirección, hay 0 voltios que van al pin, y leemos 0. Cuando el eje se gira completamente en la otra dirección, hay 5 voltios que van al pin y leemos 1023. En el medio, [analogRead()](https://www.arduino.cc/reference/en/language/functions/analog-io/analogread/) devuelve un número entre 0 y 1023 que es proporcional a la cantidad de voltaje que se aplica al pin.

```
/* Analog Read to LED
 * ------------------
 *
 * turns on and off a light emitting diode(LED) connected to digital
 * pin 13. The amount of time the LED will be on and off depends on
 * the value obtained by analogRead(). In the easiest case we connect
 * a potentiometer to analog pin 2.
 *
 * Created 1 December 2005
 * copyleft 2005 DojoDave <http://www.0j0.org>
 * http://arduino.berlios.de
 *
 */

int potPin = 2;    // select the input pin for the potentiometer
int ledPin = 13;   // select the pin for the LED
int val = 0;       // variable to store the value coming from the sensor

void setup() {
  pinMode(ledPin, OUTPUT);  // declare the ledPin as an OUTPUT
}

void loop() {
  val = analogRead(potPin);    // read the value from the sensor
  digitalWrite(ledPin, HIGH);  // turn the ledPin on
  delay(val);                  // stop the program for some time
  digitalWrite(ledPin, LOW);   // turn the ledPin off
  delay(val);                  // stop the program for some time
}

```

**Use el montaje del ejercicio uno sumando el potenciómetro**

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


## Anexos

### ¿Qué es un motor de corriente contínua?

`El motor de corriente continua, denominado también motor de corriente directa, motor CC o motor DC (por las iniciales en inglés direct current), es una máquina que convierte energía eléctrica en mecánica, provocando un movimiento rotatorio, gracias a la acción de un campo magnético.`

Un motor de corriente continua se compone principalmente de dos partes. El estátor da soporte mecánico al aparato y contiene los polos de la máquina, que pueden ser o bien devanados de hilo de cobre sobre un núcleo de hierro, o imanes permanentes. El rotor es generalmente de forma cilíndrica, también devanado y con núcleo, alimentado con corriente directa a través de delgas, que están en contacto alternante con escobillas fijas.

<iframe width="560" height="315" src="https://www.youtube.com/embed/LAtPHANEfQo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



### ¿Qué es un puente H?

<img src="https://www.inventable.eu/wp-content/uploads/2017/05/motor_dc_sentido_de_giro.png" alt="">

`
Sentido horario o anti-horario de un motor DC según la polaridad de la alimentación.
`

En los motores de corriente continua, la dirección de giro de los mismos depende de la polaridad de la alimentación. Para poder cambiar dicha polaridad, sin necesidad de invertir la batería, se pueden usar 4 interruptores conectados como indicado en la figura.

<img src="https://www.inventable.eu/wp-content/uploads/2017/05/motor_dc_puente_con_interruptores0.png" alt="">

`Puente "H" hecho con interruptores.`


Este tipo de conexión se conoce como "Puente H" (por la forma del circuito que se asemeja a la letra "H") y posee propiedades muy interesantes que veremos a lo largo de este artículo.

Si activamos el interruptor alto de la izquierda y el interruptor bajo de la derecha, el motor quedará alimentado con el positivo a la izquierda y el negativo a la derecha, por lo tanto girará en un modo (la circulación de la corriente se encuentra indicada con las líneas de color rojo y las flechas).

<img src="https://www.inventable.eu/wp-content/uploads/2017/05/motor_dc_puente_con_interruptores_giro_orario.png" alt="">

`Motor con giro horario en un puente "H" hecho con interruptores.`

<img src="https://www.inventable.eu/wp-content/uploads/2017/05/motor_dc_puente_con_interruptores_giro_antiorario.png" alt="">

`Motor con giro anti-horario en un puente "H" hecho con interruptores.`


Este sistema tiene un inconveniente: si se accionan contemporáneamente los dos interruptores de la izquierda  o los dos interruptores de la derecha se producirá un cortocircuito de la alimentación como podemos observar en la figura, por lo tanto es necesario evitar esta situación como veremos más adelante.

<img src="https://www.inventable.eu/wp-content/uploads/2017/05/motor_dc_puente_con_interruptores_corto.png" alt="">

`Cortocircuito de la alimentación en un puente "H" hecho con interruptores.`

Una condición interesante de este sistema es cuando accionamos solamente los dos interruptores de arriba, en ese caso el motor no se encuentra alimentado por la batería y además sus terminales de entrada estarán unidos entre si, a través de los interruptores. Este tipo de conexión mantiene el motor "frenado" y puede llegar a ser de utilidad en muchos casos. Lo mismo ocurre si en lugar de los dos interruptores altos, activamos ambos interruptores bajos.

<img src="https://www.inventable.eu/wp-content/uploads/2017/05/motor_dc_puente_con_interruptores_bloqueado.png" alt="">

`Motor frenado en un puente "H" hecho con interruptores.`

Naturalmente, un puente hecho solo con interruptores no es muy versátil, he dado este ejemplo para comprender en modo simple y claro el principio de funcionamiento del puente "H". Pero si reemplazamos los interruptores mecánicos por interruptores electrónicos, la cuestión se pone interesante porque estos interruptores electrónicos pueden ser activados por circuitos lógicos como por ejemplo las salidas de un microcontrolador.


## Fuente:

* http://ohhmyproject.blogspot.com/2015/09/tutorial-l293d-motor-driver-with-arduino.html
* https://www.inventable.eu/2017/05/26/funciona-puente-motores-corriente-continua/
* https://es.wikipedia.org/wiki/Motor_de_corriente_continua
* https://howtomechatronics.com/tutorials/arduino/arduino-dc-motor-control-tutorial-l298n-pwm-h-bridge/
* https://www.arduino.cc/en/tutorial/potentiometer