---
id: 5_proyecto_integrador_eje_1
title: Proyecto integrador: "Control por Gestos usando Arduino y Python"
---

## Proyecto integrador: "Control por Gestos usando Arduino y Python"

### Objetivo General

Comandar programáticamente el reproductor de Youtube mediante gestos. Leeremos los comandos desde el puerto serial enviados por Arduino y usaremos un software desarrollado en Python como interfaz.

### Materiales

- Placa Arduino Uno-R3
- Un cable USB tipo A/B de impresora
- Una computadora
- Conexión a internet
- Breadboard/Protoboard
- Jumper Wires
- 2 sensores ultrasónicos HC-SR04

### 1ra Parte: Enviar comandos con Arduino

1. Carga el siguiente programa a la placa Arduino.

```
void setup() {
  Serial.begin(9600);
}

void loop() {
  Serial.println("play_pause");
  delay(3000);
  Serial.println("rewind");
  delay(3000);
  Serial.println("forward");
  delay(3000);
  Serial.println("volume_up");
  delay(3000);
  Serial.println("volume_down");
  delay(3000);
  Serial.println("mute_unmute");
  delay(3000);
  Serial.println("mute_unmute");
  delay(3000);
  Serial.println("fullscreen");
  delay(3000);
  Serial.println("escape");
  delay(3000);
  Serial.println("captions");
  delay(3000);
  Serial.println("captions");
  delay(3000);
  Serial.println("play_pause");
  delay(3000);
}
```


***IMPORTANTE***:
Puedes visualizar los comandos enviados al puerto serial usando el monitor provisto por el IDE (Herramientas > Monitor Serial). Pero no dejes el monitor abierto porque esto bloqueara la lectura del puerto.


### 2da Parte: Interfaz en Python

***IMPORTANTE***:
Mantén conectada la placa Arduino a tu computadora.

`Requerimiento: Python 3.x`

1. Descarga el siguiente repositorio:

```
git clone https://github.com/cristianemoyano/gesture_control.git
cd gesture_control
```

2. Instala las dependencias:

```
# crea un entorno virtual en Python 3
make env

# activa el entorno creado
make activate

# instala las dependencias
make setup

# corre el programa
make run
```

Si al ejecutar `make run` ves el siguiente mensaje:

```
arduino - ERROR - Error open serial port: [Errno 2] could not open port : [Errno 2] No such file or directory: ''
```

No te preocupes, es el comportamiento esperado. Éste error se debe a que no hemos configurado el puerto con el que se va a comunicar nuestro Arduino.

3. Configuración del puerto serial:

Debemos editar la constante [SERIAL_DEVICE_NAME](https://github.com/cristianemoyano/gesture_control/blob/master/main.py#L23) con el "nombre del dispositivo serial", es decir con el puerto al que nuestro Arduino está conectado.

¿Cómo puedo listar los puertos de mi computadora? Bueno, para ello tenemos disponible el método `serial_ports` el cual lista todos los puertos disponibles de tu computadora en la consola.

**(a)** Para ejecutarlo reemplaza [éste código](https://github.com/cristianemoyano/gesture_control/blob/master/main.py#L144):
```
if __name__ == "__main__":
    read_serial(SERIAL_DEVICE_NAME)
```

**(b)** Por éste:
```
if __name__ == "__main__":
    serial_ports()
```

En la consola podrás ver los puertos disponibles:
```
...
arduino - INFO - {'device': '/dev/cu.usbmodem1411', 'name': None, 'description': 'Generic CDC', 'hwid': 'USB VID:PID=2341:0043 SER=557363235393516152B1 LOCATION=20-1', 'vid': 9025, 'pid': 67, 'location': '20-1', 'manufacturer': 'Arduino (www.arduino.cc)', 'product': 'Generic CDC', 'interface': None}

```
Podrás identificar fácilmente en cuál el puerto de nuestro Arduino.

El atributo que nos interesa es 'device' que en el ejemplo es '/dev/cu.usbmodem1411'.

**(c)** Luego nos quedaría asignar nuestra constante con el puerto encontrado:

```
SERIAL_DEVICE_NAME = '/dev/cu.usbmodem1411'
```

Finalmente deshace los cambios en el paso **(b)** y corre nuevamente el programa:

```
make run
```

Mensaje esperado:
```
arduino - INFO - Serial port opened: /dev/cu.usbmodem1411 - Baud rate: 9600 bits/second
```

**¡Muy bien! Estamos recibiendo los comandos enviados por nuestro Arduino.**


### 3ra Parte: Añadir los sensores

***El siguiente código funciona solamente para un sensor y está implementada una acción: "play_pause".***

**Actividad**:

Completa el código para que soporte 2 sensores ultrasónicos HC-SR04 e implementa las siguientes acciones:

- rewind
- forward
- volume_up
- volume_down
- mute_unmute
- fullscreen
- escape
- captions

#### Código incompleto

```
const int trigger1 = 2; //Trigger pin of 1st Sensor
const int echo1 = 3; //Echo pin of 1st Sensor
const int trigger2 = 4; //Trigger pin of 2nd Sensor
const int echo2 = 5;//Echo pin of 2nd Sensor
int distanceCm, distL, distR;

void setup() {
  Serial.begin(9600);

  pinMode(trigger1, OUTPUT);
  pinMode(echo1, INPUT);
  pinMode(trigger2, OUTPUT);
  pinMode(echo2, INPUT);
}


void loop() {
  //get distance of left sensor
  distL = calculate_distance(trigger2,echo2);

  //Play/Pause one hand
  if (distL > 8  && distL < 11 ) {
    Serial.println("play_pause");
    delay(500);
  }
}

/*###Function to calculate distance###*/
int calculate_distance(int trigger, int echo)
{
  digitalWrite(trigger, LOW);
  delayMicroseconds(2);
  digitalWrite(trigger, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigger, LOW);

  int time_taken = pulseIn(echo, HIGH);
  distanceCm = time_taken * 10 / 292/ 2;
  return distanceCm;
}
```

#### Montaje

<img src="https://circuitdigest.com/sites/default/files/circuitdiagram_mic/Control-your-Computer-with-Hand-Gestures-using-Arduino-circuit.png" alt="">

## Anexos

### Comunicación serie

La comunicación serial consiste en el envío de un bit de información de manera secuencial, ésto es, un bit a la vez y a un ritmo acordado entre el emisor y el receptor.

La comunicación serial en computadores ha seguido los estándares definidos en 1969 por el RS-232 (Recommended Standard 232) que establece niveles de voltaje, velocidad de transmisión de los datos, etc. Por ejemplo, este protocolo establece un nivel de -12v como un uno lógico y un nivel de voltaje de +12v como un cero lógico (por su parte, los microcontroladores emplean por lo general 5v como un uno lógico y 0v como un cero lógico).

Existen en la actualidad diferentes ejemplos de puertos que comunican información de manera serial (un bit a la vez). El conocido como “puerto serial” ha sido gradualmente reemplazado por el puerto USB (Universal Serial Bus) que permite mayor versatilidad en la conexión de múltiples dispositivos. Aunque en naturaleza serial, no suele referenciarse de esta manera ya que sigue sus propios estándares y no los establecidos por el RS-232.

La mayoría de los microcontroladores, entre ellos Arduino, poseen un puerto de comunicación serial. Para comunicarse con los computadores personales actuales que poseen únicamente puerto USB requieren de un dispositivo “traductor”. Arduino emplea el integrado **FT232R**, el cual es un convertidor USB-Serial. A través de este integrado el microcontrolador puede recibir y enviar datos a un computador de manera serial.

Además de realizar las conexiones físicas entre el microcontrolador y el computador, para que pueda establecerse la comunicación serial debe existir un acuerdo previo en la manera como van a ser enviados los datos. Este acuerdo debe incluir los niveles de voltaje que serán usados, el tamaño y formato de cada uno de los mensajes (número de bits que constituirán el tamaño de la palabra, existirá o no un bit de inicio y/o de parada, se empleará o no un bit de paridad), el tipo de lógica empleada (qué voltaje representará un cero o un uno), el orden en que serán enviados los datos (será enviado primero el bit de mayor peso o el de menor peso) y la velocidad de envío de datos.

Arduino facilita este proceso para que sólo sea necesario especificar la velocidad de envío de los datos. Esta velocidad es conocida como “baud rate” o rata de pulsos por segundo. Velocidades frecuentes de uso son 9600, 19200, 57600 y 115200.

### Tasa de baudios / Velocidad de transmisión (Baud rate)

La tasa de baudios (en inglés baud rate) ―también conocida como baudaje― es el número de unidades de señal por segundo. Un baudio puede contener varios bits.

<iframe width="560" height="315" src="https://www.youtube.com/embed/xWG_6SH_ft4?start=10" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Fuente:

* https://circuitdigest.com/microcontroller-projects/control-your-computer-with-hand-gestures
* https://galaxi0.wordpress.com/el-puerto-serial/
* https://es.wikipedia.org/wiki/Tasa_de_baudios