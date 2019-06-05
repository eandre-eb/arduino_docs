---
id: 2_ejercicio_dos
title: Ejercicio 2: "Ultrasonic Distance Sensor"
---

## Ejercicio 2: "Ultrasonic Distance Sensor" - Sensor ultrasónico de distancia

### Objetivo General

- En éste ejercicio vamos a aprender a utilzar el sensor ultrasónico [HC-SR04](https://cdn.datasheetspdf.com/pdf-down/H/C/-/HC-SR04-Cytron.pdf)

### Materiales

- Placa Arduino Uno-R3
- Un cable USB tipo A/B de impresora
- Una computadora
- Sensor ultrasónico HC-SR04
- Breadboard/Protoboard
- Jumper Wires

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


### Esquema de Montaje

<img src="https://www.luisllamas.es/wp-content/uploads/2015/06/arduino-ultrasonidos-montaje.png" width="500">

**Conexiones**:

El módulo ultrasónico HC-SR04 tiene 4 pins, Ground, VCC, Trig and Echo. El pint Ground y VCC necesitan ser conectados al pin de Ground y de 5 volts de la placa Arduino respectivamente y los pins trig y echo a cualquier pin Digital I/O de la placa Arduino.

* Sensor HC-SR04 conectarlo a la Breadboard
* Pin VCC del sensor conectarlo al pin +5V del Arduino
* Pin GND del sensor conectarlo al pin GND del Arduino
* Pin Trig del sensor conectarlo al pin Digital I/O #6 del Arduino
* Pin Echo del sensor conectarlo al pin Digital I/O #5 del Arduino

### Código

#### Sin librerías

Para activar el sensor necesitamos generar un pulso eléctrico en el pin Trigger (disparador) de al menos 10us. Previamente, pondremos el pin a Low durante 4us para asegurar un disparo limpio.

Posteriormente usamos la función [pulseIn](https://www.arduino.cc/reference/en/language/functions/advanced-io/pulsein/) para obtener el tiempo requerido por el pulso para volver al sensor. Finalmente, convertirmos el tiempo en distancia mediante la ecuación correspondiente.

Observar que intentamos emplear siempre aritmética de enteros, evitando usar números en coma flotante. Esto es debido a que las operaciones en coma flotante ralentizan mucho el procesador, y suponen cargar un gran número de librerías en memoria.

```
const int echoPin = 5;
const int triggerPin = 6;
long duration, distanceCm;

void setup() {
   Serial.begin(9600);
   pinMode(triggerPin, OUTPUT);
   pinMode(echoPin, INPUT);
}

void loop() {
   int cm = ping(triggerPin, echoPin);
   Serial.print("Distancia: ");
   Serial.println(cm);
   delay(1000);
}

int ping(int triggerPin, int echoPin) {
   digitalWrite(triggerPin, LOW);  //para generar un pulso limpio ponemos a LOW 4us
   delayMicroseconds(4);
   digitalWrite(triggerPin, HIGH);  //generamos Trigger (disparo) de 10us
   delayMicroseconds(10);
   digitalWrite(triggerPin, LOW);

   duration = pulseIn(echoPin, HIGH);  //medimos el tiempo entre pulsos, en microsegundos

   distanceCm = duration * 10 / 292/ 2;   //convertimos a distancia, en cm
   return distanceCm;
}
```

Para probar este código, conecta tu arduino, asegúrate de que el puerto esté correctamente configurado, verifica el código (compila) y luego cárgalo. Verás como el LED integrado a la arduino comienza a parpadear cada un segundo.

#### Con la Librería NewPing

Otra opción es emplear una librería para facilitarnos el proceso, como por ejemplo la librería [NewPing](https://playground.arduino.cc/Code/NewPing/) disponible en el gestor de librerías del IDE de Arduino.

La librería NewPing aporta funciones adicionales, como la opción de realizar un [filtro mediana](http://www.academicos.ccadet.unam.mx/jorge.marquez/cursos/imagenes_neurobiomed/Mediana_filtro.pdf) para eliminar el ruido, o **emplear el mismo pin como trigger y echo**, lo que nos permite ahorrar muchos pines en caso de tener múltiples sensores de ultrasonidos.

La librería proporciona diversos ejemplos para ilustrar su uso. El siguiente ejemplo basado en ellos, muestra el funcionamiento con un único pin para trigger y echo.


```
#include <NewPing.h>

const int UltrasonicPin = 5;
const int MaxDistance = 200;

NewPing sonar(UltrasonicPin, UltrasonicPin, MaxDistance);

void setup() {
  Serial.begin(9600);
}

void loop() {
  delay(50);                      // esperar 50ms entre pings (29ms como minimo)
  Serial.print(sonar.ping_cm()); // obtener el valor en cm (0 = fuera de rango)
  Serial.println("cm");
}
```

## Ejercicio 2.1: Sensor de distancia con alarma y LED.

### Objetivo General

- Vamos a extender el proyecto usando un Zumbador (Buzzer Activo) y un LED para detectar una distancia límite.

### Materiales adicionales

- Buzzer Activo
- LED
- Resistencia 220 Ohm


### ¿Qué es un Buzzer Activo?

<img src="https://img.staticbg.com/thumb/large/oaupload/banggood/images/AC/A4/acbca30a-61b7-4d61-b611-72a42501b713.JPG.webp" width="250" align="left">

Los buzzer activos, en ocasiones denominados zumbadores, son dispositivos que generan un sonido de una frecuencia determinada y fija cuando son conectados a tensión.

Un buzzer activo incorpora un oscilador simple por lo que únicamente es necesario suministrar corriente al dispositivo para que emita sonido. En oposición, los buzzer pasivos necesitan recibir una onda de la frecuencia.

Al incorporar de forma interna la electrónica necesaria para hacer vibrar el altavoz un buzzer activo resulta muy sencillo de conectar y controlar. Además, no suponen carga para el procesador ya que este no tiene que generar la onda eléctrica que se convertirá en sonido.

En contra posición, tienen la desventaja de que no podremos variar el tono del sonido emitido, por lo que no podremos realizar melodías, cosa que si podremos hacer con los buzzer pasivos.


Físicamente pueden ser muy parecidos, o incluso idénticos, a los buzzer pasivos, por lo que puede llegar a ser difícil determinar a simple vista si un buzzer es activo o pasivo.

Existen buzzer activos en un gran abanico de tamaños y potencias, desde tonos casi imperceptibles hasta alarmas realmente estridentes. El consumo eléctrico, lógicamente, también varia con la potencia del buzzer.

Podemos emplear los buzzer activos de menor potencia, por ejemplo, para dar avisos al usuario o proporcionar un feedback ante alguna acción, como pulsar un botón, para que el usuario compruebe que su acción ha sido recibida.

Por su parte, los buzzer de mayor potencia son adecuados para generar alarmas de forma sencilla, por ejemplo, combinados con un sensor de movimiento, un sensor de agua, o un sensor de llama, entre otros.

### Características

- Material: ABS (plástico)
- Color: Negro
- Tamaño: 9 x 11.8 mm (L x D) / 0.35 x 0.46 inch
- Voltaje nominal: 5V
- Tensión de funcionamiento: 4-8V
- Corriente nominal (MAX): 30 mA
- Min sound output at 10cm: 85 dB
- Frecuencia de resonancia: 2300±300 Hz
- Temperatura de funcionamiento: -27 to +70 °C
- Temperatura de almacenamiento: -30 to +105 °C

### Montaje

<img src="https://lh3.google.com/u/0/d/1WklsRgIqXQrclYSXZOLPwCSz_VxoqboX=w1710-h1546-iv1" width="700">

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
distance = duration * 10 / 292/ 2;

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

## Fuente:

* https://www.luisllamas.es/medir-distancia-con-arduino-y-sensor-de-ultrasonidos-hc-sr04/
* https://cdn.datasheetspdf.com/pdf-down/H/C/-/HC-SR04-Cytron.pdf
* http://www.mertarduino.com/using-ultrasonic-distance-sensor-hc-sr04-with-buzzer-led-and-arduino/2018/11/22/
* https://www.luisllamas.es/arduino-buzzer-activo/