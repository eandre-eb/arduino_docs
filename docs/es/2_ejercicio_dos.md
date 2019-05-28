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

### ¿Qué es un sensor de ultrasonido?

Un sensor de ultra sonidos es un dispositivo para medir distancias. Su funcionamiento se base en el envío de un pulso de alta frecuencia, no audible por el ser humano. Este pulso rebota en los objetos cercanos y es reflejado hacia el sensor, que dispone de un micrófono adecuado para esa frecuencia.

Midiendo el tiempo entre pulsos, conociendo la velocidad del sonido, podemos estimar la distancia del objeto contra cuya superficie impacto el impulso de ultrasonidos

Los sensores de ultrasonidos son sensores baratos, y sencillos de usar. El rango de medición teórico del sensor HC-SR04 es de 2cm a 400 cm, con una resolución de 0.3cm. En la práctica, sin embargo, el rango de medición real es mucho más limitado, en torno a 20cm a 2 metros.

Los sensores de ultrasonidos son sensores de baja precisión. La orientación de la superficie a medir puede provocar que la onda se refleje, falseando la medición. Además, no resultan adecuados en entornos con gran número de objetos, dado que el sonido rebota en las superficies generando ecos y falsas mediciones. Tampoco son apropiados para el funcionamiento en el exterior y al aire libre.

Pese a esta baja precisión, que impide conocer con precisión la distancia a un objeto, los sensores de ultrasonidos son ampliamente empleados. En robótica es habitual montar uno o varios de estos sensiores, por ejemplo, para detección de obstáculos, determinar la posición del robot, crear mapas de entorno, o resolver laberintos.

En aplicaciones en que se requiera una precisión superior en la medición de la distancia, suelen acompañarse de medidores de distancia por infrarrojos y sensores ópticos.

Existen otros sensores para detectar distancias. En distancias medias y largas tenemos el sensor óptico Sharp GP2Y0A02YK0 y en muy cortas distancias el detector de obstáculos infrarrojos.


### ¿Cómo funciona?

El sensor se basa simplemente en medir el tiempo entre el envío y la recepción de un pulso sonoro. Sabemos que la velocidad del sonido es 343 m/s en condiciones de temperatura 20 ºC, 50% de humedad, presión atmosférica a nivel del mar. Transformando unidades resulta:

<img src="https://www.luisllamas.es/wp-content/ql-cache/quicklatex.com-83780eae753d9e35a70b0ebb4f6803fa_l3.png" width="400">


Es decir, el sonido tarda 29,2 microsegundos en recorrer un centímetro. Por tanto, podemos obtener la distancia a partir del tiempo entre la emisión y recepción del pulso mediante la siguiente ecuación.

<img src="https://www.luisllamas.es/wp-content/ql-cache/quicklatex.com-9819e4766edeb37d3571e0b9656bd98d_l3.png" width="400">


El motivo de divir por dos el tiempo (además de la velociad del sonido en las unidades apropiadas, que hemos calculado antes) es porque hemos medido el tiempo que tarda el pulso en ir y volver, por lo que la distancia recorrida por el pulso es el doble de la que queremos medir.

<img src="https://www.luisllamas.es/wp-content/uploads/2015/06/sensor-ultrasonico-explicacion.png" width="400">


### ¿Qué es un buzzer activo?

Los buzzer activos, en ocasiones denominados zumbadores, son dispositivos que generan un sonido de una frecuencia determinada y fija cuando son conectados a tensión.

Un buzzer activo incorpora un oscilador simple por lo que únicamente es necesario suministrar corriente al dispositivo para que emita sonido. En oposición, los buzzer pasivos necesitan recibir una onda de la frecuencia.

Al incorporar de forma interna la electrónica necesaria para hacer vibrar el altavoz un buzzer activo resulta muy sencillo de conectar y controlar. Además, no suponen carga para el procesador ya que no este no tiene que generar la onda eléctrica que se convertirá en sonido.

En contra posición, tienen la desventaja de que no podremos variar el tono del sonido emitido, por lo que no podremos realizar melodías, cosa que si podremos hacer con los [buzzer pasivos (tmb12a05)](https://www.luisllamas.es/reproducir-sonidos-arduino-buzzer-pasivo-altavoz/).

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

Esquema de Montaje:

<img src="https://lh3.google.com/u/0/d/1WklsRgIqXQrclYSXZOLPwCSz_VxoqboX=w1710-h1546-iv1" width="700">



### Fuente:

* https://www.luisllamas.es/detectar-obstaculos-con-sensor-infrarrojo-y-arduino/
* https://www.luisllamas.es/arduino-buzzer-activo/
* http://www.mertarduino.com/using-ultrasonic-distance-sensor-hc-sr04-with-buzzer-led-and-arduino/2018/11/22/