---
id: ejercicio_uno
title: Ejercicio 1: "Blink"
---

## Ejercicio 1: "Blink" - Encender y apagar un LED

### Objetivo General

- Encender y apagar un LED con Arduino UNO R3

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
