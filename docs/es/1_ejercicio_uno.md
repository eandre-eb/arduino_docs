---
id: 1_ejercicio_uno
title: Ejercicio 1: "Blink"
---

## Ejercicio 1: "Blink" - Encender y apagar un LED

### Objetivo General

- Encender y apagar el LED incorporado con Arduino UNO R3

### Materiales

- Placa Arduino Uno-R3
- Un cable USB tipo A/B de impresora
- Una computadora


### Código

```
/*
  Blink
  Enciende un LED por un segundo y luego lo apaga por un segundo, repetidamente.
  Este código de ejemplo lo puedes encontrar en /Ejemplos/Basics/Blink en el IDE
 */

// El PIN 13 tiene un led conectado en la mayoría de las tarjetas arduino

int led = 13; // Se declara la variable led como tipo de dato entero

// La rutina setup() se ejecuta al inicio y cuando presionas el botón reset
void setup() {
  pinMode(led, OUTPUT);  //Inicializa el pin numero 13 (valor de variable led) como salida.
                         //(todas las salidas son digitales)
}
// La rutina loop() se ejecuta una y otra vez por siempre.
void loop() {
  digitalWrite(led, HIGH);   // Enciende el LED (HIGH el 1 binario o 5[V])
  delay(1000);               // Espera un segundo
  digitalWrite(led, LOW);    // Apaga el LED dejando voltaje 0[V] en la salida
  delay(1000);               // Espera por un segundo
}
```

Para probar este código, conecta tu arduino, asegúrate de que el puerto esté correctamente configurado, verifica el código (compila) y luego cárgalo. Verás como el LED integrado a la arduino comienza a parpadear cada un segundo.
Puedes cambiar la frecuencia de parpadeo cambiando el número en la función siguiente, por el número que desees.

```
delay(1000)
```

Cabe señalar que con un retardo menor a 5[ms] el ojo humano no alcanza a percibir el parpadeo y se ve como si estuviera siempre prendido. Esta característica es muy usada para ahorrar energía ya que es mejor tener el LED apagado la mitad del tiempo, que siempre encendido.

## Adicional

### Ejercicio 1.1: "Blink+" - Encender y apagar un LED externo

### Material adicional

- Resistencia de 220 k Ohm
- LED 3mm


<img src="https://i2.wp.com/mecabot-ula.org/wp-content/uploads/practica1a.png?w=507" width="600">


### Ejercicio 1.2: "Blink++" - Encender y apagar un LED externo con un pulsador

### Material adicional

- Pulsador NA (normalmente abierto)
- Resistencias de 220 k y 10k Ohm


<img src="https://lh3.google.com/u/0/d/1FlP-l_m2kakD3b24JoVRJmB-Ew4g-8kL=w2880-h1578-iv1" width="600">

* El ánodo del LED (+) conectarlo con la resistencia de 220 Ohm
* La otra pata de la resistencia conectarla al pin 2 del Arduino.
* El cátodo del LED (-) conectarlo a tierra del Arduino.
* Conectar la resistencia de 10 k en una de las patas del botón y luego esa pata a la tierra del Arduino.
* En la otra pata del botón conectarle 5v
* Conectarle en la pata superior del botón al pin 4 del Arduino


<img src="https://felixmaocho.files.wordpress.com/2013/01/pulsador-esuema1.jpg" width="150" align="left">
<img src="https://static.wixstatic.com/media/18cfef_9300efc452b74f3681dae20fd76333ea~mv2.jpg/v1/fill/w_250,h_250,al_c,q_90/file.jpg" width="150">


```
//set pin numbers
const int ledPin = 2;         //const won't change
const int buttonPin = 4;

//variables will change
int buttonState = 0;          //variables for reading the pushbutton status

void setup() {

  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);    //initialize the LED pin as an output
  pinMode(buttonPin, INPUT);  //initialize the pushbutton pin as an output
}

void loop() {

  buttonState = digitalRead(buttonPin); //read the state of the pushbutton value

  if (buttonState == HIGH) {            //check if the pushbutton is pressed
    //if it is, the buttonState is HIGH
    digitalWrite(ledPin, HIGH);         //turn LED on
    Serial.println("LED ON +++++++");
  }
  else {

    digitalWrite(ledPin, LOW);          // turn LED off
    Serial.println("LED OFF -------");
  }

}
``

## Anexos

### ¿Qué es un LED?

<img src="https://upload.wikimedia.org/wikipedia/commons/c/c0/LED%2C_5mm%2C_green_%28en%29.png" width="400" align="left">

Un LED , es un dispositivo diodo emisor de luz que se usan como indicadores en muchos dispositivos y en iluminación. Los primeros LEDs emitían luz roja de baja intensidad, pero los dispositivos actuales emiten luz de alto brillo en el espectro infrarrojo, visible y ultravioleta. Un LED comienza a funcionar aproximadamente con 2 voltios.

#### ¿Cómo determino la polaridad de un LED?

Existen tres formas principales de conocer la polaridad de un led:

* La pata más larga siempre va a ser el ánodo.
* En el lado del cátodo, la base del LED tiene un borde plano.
* Dentro del LED la plaqueta indica el ánodo. Se puede reconocer porque es más pequeña que el yunque que indica el cátodo.

### ¿Qué es una Protoboard/Breadboard?

<img src="https://http2.mlstatic.com/protoboard-830-puntos-placa-experimental-arduino-electronica-D_NQ_NP_844461-MLA30225042449_052019-Q.jpg" width="400">
(Protoboard solderless de 830 puntos con doble banda de alimentación en ambos lados.)

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4f/Pcb33.430-g1.jpg/400px-Pcb33.430-g1.jpg" width="350">
(Protoboard de 400 puntos)

Es un tablero con orificios conectados eléctricamente entre sí, habitualmente siguiendo patrones de líneas, en el cual se pueden insertar componentes electrónicos y cables para el armado de prototipos de circuitos electrónicos y sistemas similares. Está hecho de dos materiales, un aislante, generalmente un plástico, y un conductor que conecta los diversos orificios entre sí. Uno de sus usos principales es la creación y comprobación de prototipos de circuitos electrónicos antes de llegar a la impresión mecánica del circuito en sistemas de producción comercial.

[Wiki](https://en.wikipedia.org/wiki/Breadboard)

### ¿Qué es una resistencia/resistor?

<img src="http://telesaonline.com/49228-large_default/resistencia-carbon-1-4w-20k-ohms.jpg" width="300" align="left">

La resistencia o resistor, es cualquier elemento localizado en el paso de la corriente eléctrica y que causa oposición a que esta fluya. Las resistencias se representan con la letra R y se miden en Ohm (Ω). Para obtener el valor de una resistencia, se puede emplear:

* [Una tabla](https://www.inventable.eu/media/122_Resistencias_colores/resistor_color_4band.png) o [una calculadora online](https://www.digikey.com/es/resources/conversion-calculators/conversion-calculator-resistor-color-code-5-band)
* Un multímetro

En las resistencias existen 3 características fundamentales:

- el valor de resistencia ([Ohm] R = V/I)
- la potencia ([Watt] P = V.I)
- la tolerancia (%)

A excepción de la potencia que depende de las dimensiones de las resistencias, el valor de resistencia y la tolerancia son indicados con bandas de color. Existen dos tipo de codificación para las resistencias con bandas de color: la de 4 bandas o la de 5 bandas para las resistencias de precisión. En ambos sistemas, la última banda indica la **tolerancia**, es decir cual es la variación que el valor real de resistencia puede diferir respecto al indicado en el cuerpo. En la codificación de 4 bandas, si falta la banda de tolerancia quiere decir que la tolerancia es de +/- el 20% y por lo tanto veremos solo 3 bandas.

La potencia de una resistencia determina la cantidad de Watts que soporta. Se puede calcular mediante la siguiente fórmula:
```
P = V . I

// Ejemplo: En un circuito donde circula una corriente de 20mA
// con una fuente de alimentación de 5v la potencia es de:

P = V.I = 5 x 0.02 = 0.1 W

// Por lo tanto la resistencia que debo elegir es de al menos de 1/8 W = 0.125 W
// Menos potencia podría causar que se queme la resistencia y mayor potencia estaría demás.
```

## Enlaces

* https://www.tinkercad.com/
